# unordered_map

- 정렬이되지 않은 map
- 메서드는 map과 동일
- 해시테이블 기반
- 참색, 삽입, 삭제에 평균적으로 O(1)
- 가장 최악의 경우 O(N)
- 그냥 최대한 map을 쓰자
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    unordered_map<string, int> umap;
    int main(){
      umap["bcd"] = 1;
      umap["aaa"] = 1;
      umap["aba"] = 1;
      for(auto it : umap) cout << it.first << " : " << it.second << "\n";
      return 0;
    }
    /*
    aba : 1
    aaa : 1
    bcd : 1
    */
    ```