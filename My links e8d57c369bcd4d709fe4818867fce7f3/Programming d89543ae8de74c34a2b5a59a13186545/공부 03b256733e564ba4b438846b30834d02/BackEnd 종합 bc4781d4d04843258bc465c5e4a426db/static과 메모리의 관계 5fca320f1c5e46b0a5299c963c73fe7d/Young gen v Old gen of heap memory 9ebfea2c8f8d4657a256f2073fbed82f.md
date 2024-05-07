# Young gen v. Old gen of heap memory

힙(Heap) 메모리는 자바 프로그램에서 동적으로 할당되는 객체와 배열이 저장되는 영역입니다. 힙은 Young Generation(젊은 세대)과 Old Generation(늙은 세대) 두 가지 세대로 나뉩니다.

1. **Young Generation(젊은 세대)**:
    - 새로 생성된 객체들이 할당되는 영역입니다.
    - Young Generation은 Eden 영역과 두 개의 Survivor 영역(Survivor 0, Survivor 1)으로 나뉩니다.
    - 새로운 객체들은 Eden 영역에 할당됩니다. Eden 영역이 가득 차면, Eden 영역에 있는 객체들 중에서 살아남은 객체들은 Survivor 영역 중 하나로 이동합니다.
    - GC(Garbage Collector)가 실행될 때, Eden 영역과 첫 번째 Survivor 영역에 있는 객체들 중에서 더 오래된 객체들은 다른 Survivor 영역으로 이동하거나 Old Generation으로 이동합니다.
    - Survivor 영역들 간에는 객체들의 이동이 반복되며, 오래된 객체들은 Old Generation으로 이동됩니다.
2. **Old Generation(늙은 세대 또는 세대별 영역)**:
    - Young Generation에서 일정 시간 동안 살아남은 객체들이 이동하는 영역입니다.
    - Old Generation에 있는 객체들은 주로 오랜 시간 동안 살아남아 계속해서 사용되는 객체들입니다.
    - Old Generation은 Young Generation보다 GC의 주기가 길고, GC가 실행될 때마다 많은 수의 객체들이 동시에 처리됩니다.
    - Old Generation에 있는 객체들 중에서 더 이상 사용되지 않는 객체들은 GC에 의해 제거됩니다.

Young Generation과 Old Generation은 GC 알고리즘에 따라 다르게 관리되며, 메모리 사용량과 GC의 주기에 따라 동적으로 조정됩니다. 이러한 메모리 구조는 자바 프로그램의 성능과 메모리 관리에 중요한 역할을 합니다.

![Untitled](Young%20gen%20v%20Old%20gen%20of%20heap%20memory%209ebfea2c8f8d4657a256f2073fbed82f/Untitled.png)

Garbage Collector가 Heap 메모리 영역을 돌면서 다른 식별자에 의해 참조되고 있지 않으면 메모리를 해제 시키고 아직도 식별되고 있다면 카운트를 올리는 방식으로 객체가 얼마나 오랫동안 공간을 차지하고 있었는지 파악한다.