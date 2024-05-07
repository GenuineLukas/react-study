# priority queue

- 각 요소에 어떠한 우선순위가 추가로 부여되어있는 컨테이너
- greater<T>를 써서 오름짜순, less<T>을 써서 내림차순으로 바꿀 수 있다
- 기본값은 **내림차순**이다.

```cpp
#include <bits/stdc++.h>
using namespace std;
priority_queue<int, vector<int>, greater<int>> pq; //오름차순
priority_queue<int> pq2;//내림차순
priority_queue<int, vector<int>, less<int>> pq3;//내림차순

int main() {
  for(int i = 5; i>=1; i--){
    pq.push(i); pq2.push(i); pq3.push(i);
  }
  while(pq.size()){
    cout << pq.top() << " : " << pq2.top() << " : " << pq3.top() << "\n";
    pq.pop(); pq2.pop(); pq3.pop();
  }
  return 0;
}
/*
1 : 5 : 5
2 : 4 : 4
3 : 3 : 3
4 : 2 : 2
5 : 1 : 1
*/
```

**구조체를 담은 우선순위큐**

우선순위큐에 커스텀 정렬을 넣을 때는 **반대라고 생각**하면 된다. 가장 최소를 끄집어 내고 싶은 로직이라면 >, 최대라면 < 이런식으로 설정하면 된다.

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Point{
  int y, x;
  Point(int y, int x) : y(y), x(x){}
  Point(){y=-1; x=-1;}
  bool operator < (const Point & a) const{
    return x > a.x;
  }
};

priority_queue<Point> pq;
int main(){
  pq.push({1, 1});
  pq.push({2, 2});
  pq.push({3, 3});
  pq.push({4, 4});
  pq.push({5, 5});
  pq.push({6, 6});
  cout << pq.top().x << "\n"; //1
  return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Point{
  int y, x;
  Point(int y, int x) : y(y), x(x){}
  Point(){y=-1; x=-1;}
  bool operator < (const Point & a) const{
    return x < a.x;
  }
};

priority_queue<Point> pq;
int main(){
  pq.push({1, 1});
  pq.push({2, 2});
  pq.push({3, 3});
  pq.push({4, 4});
  pq.push({5, 5});
  pq.push({6, 6});
  cout << pq.top().x << "\n"; //6
  pq.pop();
  return 0;
}
```