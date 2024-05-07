# C++ Data Structures

[comp (operator overloading)](https://tokkic.tistory.com/67)

[vectors](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/vectors%202006fd5acf794c7b8bbc79fc0e819776.md)

[array](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/array%2090cf6d8dc9f645c8ad87735c18d86831.md)

[list](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/list%208915a92ed88c4ccc94f653e784fe3ee7.md)

- vector, array와 같은 배열은 램덤 접근이 가능해서 k번째 요소에 접근할 때 O(1)이 걸리며 연결리스트, 스택, 큐는 순차적 접근이 가능해서 k번째 요소에 접근할 때 O(k)이 걸린다.
- Array v. LinkedList
    1. 배열은 연속된 메모리 공간에 데이터를 저장, 연결리스트는 연속되지 않은 메모리 공간에 데이터를저장.
    2. 배열: 삽입,삭제(O(N)), 참조(O(1)) // 연결리스트: 삽입,삭제(O(1)), 참조(O(N))
    3. 데이터 추가와 삭제가 많다. → 리스트를 써라. // 참조를 많이 한다 → 배열을 써라.

[map](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/map%20ef1ed2ca3d6642a88e2ebb4a3e8b9dd2.md)

[unordered_map](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/unordered_map%2086be28e6aaef44af89a2348c131c197c.md)

[set](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/set%200ab9e28bed4a4b0c9121257f1395cbc1.md)

[multiset](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/multiset%204f7ca0354f32439da74e18d6ff20a955.md)

[stack](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/stack%20015924e9e70047829c5bde88f2b25841.md)

[queue](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/queue%20b7bd5e3f308c46e6add63530f0cb597f.md)

[dequeue](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/dequeue%2092d34991edfc46e498008dd16b9bda2c.md)

[struct](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/struct%20c2e4f42964084866a1bb29d9ca5e8869.md)

[priority queue](C++%20Data%20Structures%2058d75dc8bf454d7aa0f0da499372410f/priority%20queue%20abff34ebc4e240f1a5d3893d01f36c0c.md)

**최악의 시간 복잡도**

| 자료구조 | 참조 | 탐색 | 삽입 | 삭제 |
| --- | --- | --- | --- | --- |
| 배열 | O(1) | O(n) | O(n) | O(n) |
| 스택 | O(n) | O(n) | O(1) | O(1) |
| 큐 | O(n) | O(n) | O(1) | O(1) |
| 연결리스트 | O(n) | O(n) | O(1) | O(1) |
| 맵 | O(logN) | O(logN) | O(logN) | O(logN) |