~~사실은 내가 파헤쳐지기......~~

# 📁 domain package
## 🅒 Member Class

```java
package study.spring.domain;

public class Member {

//private 접근제어자로 Member의 속성 id와 Name을 선언
    private Long id;
    private String name;

//getter setter
    public Long getId() {
        return id;
    } //Id를 반환
    public void setId(Long id) {
        this.id = id;
    } // id를 받아와 값을 초기화 해줌

//getter setter
    public String getName() {
        return name;
    } //name을 반환
    public void setName(String name) {
        this.name = name;
    } // name을 받아와 값을 초기화 해줌

}
```

---

# 📁 repository package
## ⓘ MemberRepository Interface

```java
package study.spring.repository;

import study.spring.domain.Member;

import java.util.List;
import java.util.Optional;

public interface MemberRepository {
// MemberRepository 인터페이스. 내부의 메서드에는 구현부가 없고 선언부만 있다.
// 이 인터페이스를 구현하는 클래스에서 각각의 메서드들을 오버라이드해 구현부를 작성한다.

    Member save(Member member);


    // * Optional : 자바 8부터 지원
    // Optional로 감싸준 Member 객체에는 null 값이 들어올 수 없다.
    // NPE(NullPointerException) 예외처리를 하지 않아도 됨.
    // - NPE는 자주 발생하는 Exception이다!

    Optional<Member> findById(Long id); //Id로 찾는 메서드

    Optional<Member> findByName(String name); //이름으로 찾는 메서드

    List<Member> findAll(); //모든 회원 조회
}
```

## 🅒 MemoryMemberRepository Class
```java
package study.spring.repository;

import study.spring.domain.Member;

import java.util.*;

public class MemoryMemberRepository implements MemberRepository {
//MemberRepository 인터페이스를 구현하는 MemoryMemberRepository 클래스


    // Long이라는 key값 - DB에서 PK와 비슷한 역할을 한다.
    // Member라는 value 값 - 여기서 Member는 객체다.
    private static Map<Long,Member> store = new HashMap<>();
    
    //시퀀스의 초기 값을 0으로 초기화해주었다.
    private static long sequence = 0L;


    @Override
    public Member save(Member member) {
    //Member 자료형의 member를 파라미터로 받아 저장하는 메서드
        member.setId(++sequence);
        //member 한 명이 회원가입을 할 때마다 pk값을 1씩 증가
        store.put(member.getId(), member);
        //게터로 Id를 받아와 member에 삽입
        return member;
        //
    }

    //아이디로 단건조회.
    //여기서 같은 시퀀스인 멤버는 존재할 수 없기 때문에 단건 조회가 가능하다.
    @Override
    public Optional<Member> findById(Long id) {
        return Optional.ofNullable(store.get(id));
    }

    //이름으로 단건조회
    @Override
    public Optional<Member> findByName(String name) {
        return store.values().stream()
                .filter(member -> member.getName().equals(name))
                //filter : stream 내 요소를 필터링해준다.
                //getName()으로 받아온 이름 정보가 member와 같으면
                .findAny();
                //조건에 일치하는 요소 하나를 리턴
    }


    //모든 value를 반환한다.
    @Override
    public List<Member> findAll() {
        return new ArrayList<>(store.values());
    }


    //모두 삭제한다.
    public void clearStore() {
        store.clear();
    }
}

// TDD(테스트 주도 개발)
// domain - repository - service - controller
//layer(계층)
```

---

# 📁 service package
## 🅒 MemberService Class
```java
package study.spring.service;

import study.spring.domain.Member;
import study.spring.repository.MemberRepository;

import java.util.List;
import java.util.Optional;

public class MemberService {
// 위의 service는 repository보다 브라우저와 더 가깝다.

    //DI(Dependency Injection) : 의존성 주입
    private final MemberRepository memberRepository;

//MemberRepository 자료형의 memberRepository를 매개변수로 받아와 값을 초기화하는 메서드
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    // 회원가입
    public Long join(Member member) {
        vaildationDuplicateMember(member);
        // 중복을 확인하는 메서드
        
        memberRepository.save(member);

        return member.getId();
    }

    //중복 확인
    private void vaildationDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(m -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                    //Controller의 @RequestMapping의 값이 중복되어 나타나는 에러
                });
    }

    //전체 회원 조회
    public List<Member> findMembers() {
    //return 자료형이 List<Member>인 findMembers() 메서드
        return memberRepository.findAll();
        //전체 회원을 조회한다.
    }

    //단건 조회
    public Optional<Member> findOne(Long memberId) {
    //memberId를 매개변수로 받아와 Id로 회원을 단건 조회한다.
        return memberRepository.findById(memberId);
    }
}

```

---

# 📁 test - repository package
## 🅒MemoryMemberRepositorTest Class
```java
package study.spring.repository;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;
import study.spring.domain.Member;
import study.spring.repository.MemoryMemberRepository;

import java.util.List;

import static org.assertj.core.api.AssertionsForClassTypes.assertThat;

class MemoryMemberRepositoryTest {

    MemoryMemberRepository memberRepository = new MemoryMemberRepository();

    //테스트케이스가 다 실행된 후 실행되는 메서드
    @AfterEach
    public void afterEach() {
        memberRepository.clearStore();
    }

    @Test
    public void save() throws Exception{
        //given
        Member member = new Member();
        member.setName("Spring");
        //회원 이름은 Spring, ID는 자동으로 1씩 증가함 (회원이 늘어날 때 마다)

        //when
        memberRepository.save(member); //회원저장

        //then
        Member result = memberRepository.findById(member.getId()).get();

        //만약 내가 저장한 회원이랑, findById로 찾은 회원이랑 일치한다면 테스트케이스 성공
        assertThat(result).isEqualTo(member);
    }

    @Test
    public void findByName() throws Exception {
        //given
        //이름이 Spring1인 회원 저장
        Member member1 = new Member();
        member1.setName("Spring1");
        memberRepository.save(member1);

        //이름이 Spring2인 회원 저장
        Member member2 = new Member();
        member2.setName("Spring2");
        memberRepository.save(member2);

        //when
        //이름이 Spring1인 회원 조회
        Member result = memberRepository.findByName("Spring1").get();

        //then
        //만약 조회한 회원과 member1이 같다면 테스트케이스 성공
        assertThat(result).isEqualTo(member1);

    }

    //전체조회
    @Test
    public void findAll() throws Exception {

        //given
        Member member1 = new Member();
        member1.setName("Spring1");
        memberRepository.save(member1);

        Member member2 = new Member();
        member2.setName("Spring2");
        memberRepository.save(member2);

        //when
        //저장한 회원 모두 조회
        List<Member> result = memberRepository.findAll();

        //then
        //저장된 회원의 수는 2명임 만약 회원을 저장한 List의 크기가 2라면 테스트케이스 성공
        assertThat(result.size()).isEqualTo(2);
    }
}

```
# 📁 test - service package
## 🅒 MemberServiceTest
```java
package study.spring.service;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import study.spring.domain.Member;
import study.spring.repository.MemoryMemberRepository;

import static org.assertj.core.api.AssertionsForClassTypes.assertThat;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;

public class MemberServiceTest {

    // DI
    MemberService memberService;
    MemoryMemberRepository memberRepository;

    @BeforeEach
    //테스트케이스 실행 전
    public void beforeEach() {
        memberRepository = new MemoryMemberRepository();
        //MemorymemberRepository를 만든다.
        memberService = new MemberService(memberRepository);
        //MemberService의 memberRepository에 넣어줌.
    }

    @AfterEach
    //테스트케이스 실행 후, DB의 값을 모두 삭제
    public void afterEach() {
        memberRepository.clearStore();
    }

    @Test
    public void 회원가입() throws Exception {
        // given
        Member member = new Member();
        member.setName("hello");

        // when
        Long saveId = memberService.join(member);

        // then
        Member findMember = memberRepository.findById(saveId).get();
        assertEquals(member.getName(), findMember.getName());
    }

    @Test
    public void 중복회원예외() throws Exception {
        // given
        // 고의적으로 member1의 이름과 member2의 이름을
        // Spring으로 중복 시켰다.
        Member member1 = new Member();
        member1.setName("Spring");

        Member member2 = new Member();
        member2.setName("Spring");

        // when
        memberService.join(member1);
        //member1이 회원가입을 함

        // Spring으로 이름이 같은 회원으로 회원가입을 시도했기 때문에 예외가 생길 수 밖에 없다.
        // 에외가 발생해야 정상!
        IllegalStateException e = assertThrows(IllegalStateException.class,
                () -> memberService.join(member2));

        // then
        assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다.");
    }
}

```
