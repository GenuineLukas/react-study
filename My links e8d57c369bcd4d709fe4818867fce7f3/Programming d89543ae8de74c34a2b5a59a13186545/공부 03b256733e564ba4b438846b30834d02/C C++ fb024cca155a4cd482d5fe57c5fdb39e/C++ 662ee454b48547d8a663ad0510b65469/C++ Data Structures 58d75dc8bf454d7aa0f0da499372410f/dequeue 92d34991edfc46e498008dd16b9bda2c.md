# dequeue

- 앞뒤로삽입, 삭제, 참조가 가능

```cpp
#include <bits/stdc++.h>
using namespace std;

deque<int> dq;
int main() {
  dq.push_front(1);
  dq.push_back(2);
  dq.push_back(3);
  cout << dq.front() << "\n"; //1
  cout << dq.back() << "\n"; //3
  cout << dq.size() << "\n"; //3
  dq.pop_back();
  dq.pop_front();
  cout << dq.size() << "\n"; //1
  return 0;
}
```