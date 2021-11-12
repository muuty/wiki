
# Effective go
- effective go를 읽고 정리합니다.


## Formatting
- Go에서는 컴퓨터가 대부분의 포맷팅 이슈를 처리하도록 하는 접근법을 취한다.
- gofmt이 들여쓰기, 수직 줄맞춤, 주석 포맷팅 등을 표준 스타일로 변경해준다.
- 들여쓰기는 탭을 사용한다.
- 줄 길이에는 제한이 없다.

## Commentary
- godoc은 코드가 포함하는 내용을 문서화하여 노출해준다. 이 때 주석도 추출하여 설명 문서로 제공해준다.
- 선언부 이전에 주석을 된다.
- 모든 패키는 패키지 구문 이전에 "패키지 주석"을 가지는 게 좋다.
    - 패키지가 간단한 것이면 패키지 주석도 간단하게 작성하면 된다.
- 설명하려는 선언부의 이름으로 주석을 시작해라
    - 예시 - func Compile() : //Compile parses a regular ..

## Names
- Go에서는 이름의 첫 글자가 대문자인지 소문자인지에 따라 패키지 밖에서의 노출 여부가 정해진다.
- 관례적으로, 패키지명은 소문자, 한 단어로만 부여하며 언더바(_)나 대소문자 혼용에 대한 필요가 없어야한다.
- 패키지 이름을 네이밍에 활용하라. 예를 들면, bufio 패키지에 있는 버퍼 리더는 BufReader가 아닌 Reader로 불린다. bufio.Reader가 bufio.BufReader보다 명확하고 간결하기 때문이다.
- getter 메서드에 Get은 쓰지 않는다. 예를 들면, obj.GetOwner() 대신 obj.Owner()를 쓴다.
- 언더바를 쓰지 않고 MixedCaps 혹은 mixedCaps로 쓴다.

## Semicolons
- Go에서는 구문분석기(lexer)가 간단한 규칙을 사용하여 자동으로 세미콜론을 삽입한다.
- 규칙을 간단하게 설명하면, "구문을 끝낼 수 있는 토큰 뒤에 새로운 라인이 오면, 세미콜론을 삽입하라"이다.
- 주의할 것은 제어문을 여는 중괄호를 다음 라인에 사용하지 말아야 한다는 것이다. 예를 들면, 다음과 같이 코드를 쓰면 세미콜론이 의도하지 않은 곳에 추가될 것이다.
```
if i < f()  // wrong!
{           // wrong!
    g()
}
```


## Control Structures
- go언어에는 do나 while이 존재하지 않는다. 대신, 좀 더 일반화된 for문과 유연한 switch문이 존재한다.
- For문은 다음 세 가지 형태로 사용할 수 있다.
```
// C언어와 같은 경우
for init; condition; post { }

// C언어의 while 처럼 사용
for condition { }

// C언어의 for(;;) 처럼 사용
for { }
```
- if else if else를 반복하여 작성하는 것보다 switch를 사용하는 것이 더 Go 언어답다. 다음처럼 사용할 수 있다.
```

func unhex(c byte) byte {
    switch {
    case '0' <= c && c <= '9':
        return c - '0'
    case 'a' <= c && c <= 'f':
        return c - 'a' + 10
    case 'A' <= c && c <= 'F':
        return c - 'A' + 10
    }
    return 0
}
```

- 인터페이스 변수의 동적 타입을 사용할 때 switch를 사용할 수 있다.
```

var t interface{}
t = functionOfSomeType()
switch t := t.(type) {
default:
    fmt.Printf("unexpected type %T\n", t)     // %T prints whatever type t has
case bool:
    fmt.Printf("boolean %t\n", t)             // t has type bool
case int:
    fmt.Printf("integer %d\n", t)             // t has type int
case *bool:
    fmt.Printf("pointer to boolean %t\n", *t) // t has type *bool
case *int:
    fmt.Printf("pointer to integer %d\n", *t) // t has type *int
}
```

## Functions
- Go 언어가 가지고 있는 특징 중 하나는 함수와 메소드가 여러 값을 반환 할 수 있다는 것이다.
- 아래와 같은 형태는 지극히 일반적이다.
```
func (file *File) Write(b []byte) (n int, err error)
```
- 이름 있는 결과 (Named result parameters)를 반환하는 것이 가능하다.
- 결과에 이름을 부여하면 코드를 더 짧고 명확하게 만들어 주며, 문서화가 된다.
```
func ReadFull(r Reader, buf []byte) (n int, err error) {
    for len(buf) > 0 && err == nil {
        var nr int
        nr, err = r.Read(buf)
        n += nr
        buf = buf[nr:]
    }
    return
}
```
