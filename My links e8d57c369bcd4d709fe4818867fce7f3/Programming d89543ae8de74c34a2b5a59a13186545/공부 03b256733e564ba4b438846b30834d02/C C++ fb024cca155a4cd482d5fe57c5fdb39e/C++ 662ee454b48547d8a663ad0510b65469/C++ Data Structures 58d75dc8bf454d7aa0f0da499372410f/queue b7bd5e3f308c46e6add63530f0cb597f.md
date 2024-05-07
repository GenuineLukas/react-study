# queue

- FIFO
- 삽입/삭제: O(1), 탐색: O(N)

![Untitled](queue%20b7bd5e3f308c46e6add63530f0cb597f/Untitled.png)

```cpp
#include <bits/stdc++.h>
using namespace std;

queue<int> q;
int main() {
  for(int i = 1; i <= 10; i++) q.push(i);
  while(q.size()){
    cout << q.front() << ' ';
    q.pop();
  }
  /*
  1 2 3 4 5 6 7 8 9 10
  */
  return 0;
}
```