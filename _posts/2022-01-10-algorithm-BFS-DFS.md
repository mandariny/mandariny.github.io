---
layout: single
title: "[Algorithm] BFS / DFS"
---

**key word** : BFS, DFS, 너비 우선 탐색, 깊이 우선 탐색, Queue, Stack

<br><br>

- [바킹독님의 유튜브](https://www.youtube.com/watch?v=ftOmGdm95XI&list=PLtqbFd2VIQv4O6D6l9HcD732hdrnYb6CY&index=10) 및 가지고 있던 알고리즘 책들을 참고하여 정리한 내용
- 새로 이해하는 내용이 생기거나 알고리즘 문제를 접하면서 알게 되는 내용들이 생기면 계속 추가할 예정

## BFS

1. 정의

   - 그래프 혹은 다차원 배열에서 각 칸을 방문할 때 너비를 우선하여 탐색하는 알고리즘
   - 인접한 칸 중 방문한 곳을 Queue에 넣고 Queue의 front에서부터 pop을 하며 방문한 칸을 늘려가는 방법

2. 특징

   - <mark>Queue</mark> 자료구조를 사용
   - 모든 칸에 한 번씩 방문하게 되므로 O(n)의 복잡도를 갖게 됨
   - 인근 그래프(혹은 배열)을 탐색할 때 사용하고, 최단거리를 구할 때 사용할 수 있음

3. 자바구현

   - C++에는 Pair란 자료구조가 있는 것 같지만 자바에는 따로 없으므로 Pair라는 class를 만들어서 사용해줬다.
   - int형의 x, y라는 멤버변수와 생성자만 가지고 있는 간단한 클래스이므로 코드는 생략한다.
   - 배열의 사이즈와 내용을 입력받는 부분도 생략했다.

   ```
       import java.util.LinkedList;
       import java.util.Queue;

       public class BFS {

           public static void main(String[] args) {

               Queue<Pair> queue = new LinkedList<>();

               // N x M 사이즈 이차원 배열을 입력받는다고 가정한다
               int[][] map = new int [N][M];
               boolean[][] visited = new boolean[N][M];

               // 인접한 칸에 방문하기 위해 사용하는 배열
               int[] x_axis = {1,0,-1,0};
               int[] y_axis = {0,1,0,-1};

               // 시작점을 큐에 넣어줄 때 꼭 방문 표시도 해줘야 한다
               queue.offer(new Pair(0, 0));
               visited[0][0] = true;

               // 큐가 다 빌 때까지 반복
               while(!queue.isEmpty()) {
                   Pair p = queue.poll();

                   int x = p.x;
                   int y = p.y;

                   // 방문 순서를 나타내기 위한 출력
                   System.out.println(x+", "+y+" -> ");

                   // 인접한 칸을 돈다
                   for(int i = 0; i < 4; i++) {
                       int cx = x + x_axis[i];
                       int cy = y + y_axis[i];

                       // 방문하려는 칸이 배열의 범위 내인지 확인
                       if(cx <0 || cx >= N || cy < 0 || cy >= M)
                           continue;
                       // 이미 방문한 적 있는 칸이 아닌지 확인
                       if(map[cx][cy] != 1 || visited[cx][cy] == true)
                           continue;

                       // 범위 내의 방문한 적 없는 칸이라면, 큐에 넣고 방문 표시
                       queue.offer(new Pair(cx,cy));
                       visited[cx][cy] = true;
                   }
               }

           }

       }
   ```

4. 주의해야 할 점
   - 시작점의 방문 표시를 안하는 경우
   - Queue에 넣을 때가 아니라 뺄 때 방문 표시를 하는 경우
     <br>
     -> 같은 칸이 Queue에 여러 번 쌓여 시간과 메모리가 낭비될 수 있음
   - 방문 가능한 범위 체크를 잘못하는 경우
5. 자주 사용되는 응용 유형
   - Flood Fill
   - 거리 측정
   - 시작점이 여러 개인 경우
   - 시작점이 두 종류인 경우
   - 1차원에서 BFS를 사용할 때

## DFS

1. 정의
   - 그래프 혹은 다차원 배열에서 각 칸을 방문할 때 깊이를 우선하여 탐색하는 알고리즘
   - 인접한 칸 중 방문한 곳을 Stack에 넣고 Stack의 top부터 방문한 칸을 늘려가는 방법
   - 한 방향으로 수직하게 깊이 탐색하며 전체를 탐색하는 알고리즘
2. 특징
   - <mark>Stack</mark> 자료구조를 사용
   - 모든 칸에 한 번씩 방문하게 되므로 O(n)의 복잡도를 갖게 됨
   - 인근 그래프(혹은 배열)을 탐색할 때 사용할 수 있지만 BFS와 달리 배열에서의 최단거리를 구할 수는 없음. 단, 그래프나 트리 자료구조에서 활용 가능.
