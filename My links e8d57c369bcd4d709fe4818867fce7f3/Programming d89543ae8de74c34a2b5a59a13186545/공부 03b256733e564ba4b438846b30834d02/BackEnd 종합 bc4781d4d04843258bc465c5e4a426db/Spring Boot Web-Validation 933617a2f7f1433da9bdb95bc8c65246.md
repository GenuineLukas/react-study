# Spring Boot Web-Validation

프로젝트 셋팅 (dependency에 validation 추가)

![Untitled](Spring%20Boot%20Web-Validation%20933617a2f7f1433da9bdb95bc8c65246/Untitled.png)

밸리데이션을 요청 하는 변수의 개수가 많아지게 되면 유효성 검증을 하는 코드의 길이가 너무 길어진다.

이는 service 로직에 방해가 되고, 흩어져 있는 경우 어디서 검증 되었는지 찾기 힘들다. 검증 로직이 변경되는 경우 테스트 코드 등, 전 체 로직이 흔들릴 수 있다.

| 어노테이션  | 능력 | 부가사항 |
| --- | --- | --- |
| @size | 문자 길이 측정 | Int type 불가 |
| @NotNull | null 불가 |  |
| @NotEmpty | null, “” 불가 |  |
| @NotBlank | null, “”, “ “ 불가 |  |
| @Pattern | 정규식 적용 |  |
| @Max | 최대값 |  |
| @Min | 최소값 |  |
| @AssertTrue / False | 별도 Logic 적용 |  |
| @Valid | 해당 object validation 실행 |  |
| @Past | 과거 날짜 |  |
| @PastOrPresent | 오늘이거나 과거 날짜 |  |
| @Future | 미래 날짜 |  |
| @FutureOrPresent | 오늘이거나 미래 날짜 |  |