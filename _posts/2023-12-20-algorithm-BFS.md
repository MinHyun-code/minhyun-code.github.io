---
layout: post
title: "BFS - 너비 우선 탐색"
subtitle: "Breadth-First Search"
category: "algorithm"
date: 2023-12-20
background: '/img/posts/codeImg.jpg'
---


<br> 
<br> 
<br>

# BFS (Breadth First Search)

가까운 노드부터 우선적으로 탐색, 최단 경로 또는 임의의 경로를 찾고자 할 때 사용

`Queue를 사용하여 구현`

<br>
<br>

## 특징

- 직관적이지 않다. (단계별 탐색)
- 재귀적으로 동작하지 않는다.
- 그래프 탐색의 경우, 어떤 노드를 방문했는지 그 여부를 반드시 검사해야 한다. (무한루프 방지) 

<br>
<br>

## 로직

![aspect](/blog/img/posts/BFS1.png)

<br>

> 위 그래프의 간선은 양방향
> 
> 탐색할 노드를  1로 잡는다면, 아래와 같은 과정을 거친다.
>
> 1. 큐에 1번 노드를 넣고 방문했음을 표시한다.
> 2. 1번과 인접한 노드를 큐에 넣고 방문 처리한다. (2, 3, 7)
> 3. 큐에서 노드 하나를 꺼낸다. (FIFO 이므로 1번 노드)
> 4. 인접한 노드가 없으면 3번 과정으로 돌아간다.
> 5. 인접한 노드가 있고 방문하지 않았다면 큐에 넣고 방문 처리 후 3번 과정으로 돌아간다.
> 6. 큐가 빌 때까지 반복한다.
> 
> `결과 값 1 -> 2 -> 3 -> 7 -> 5 -> 6 -> 4 -> 8`

<br>
<br>

## 구현

<br>

```java
public class My_BFS {
    public static void main(String[] args) {

        // 그래프를 2차원 배열로 표현
        // 인덱스와 노드를 일치 시키기 위해 0은 저장하지 않음
        // 1번 인덱스 = 1번 노드, 배뎔의 값은 연결된 노드
        int[][] graph = { {}, {2,3,7}, {1,3,5}, {1,2}, {6,8}, {2}, {4,7,8}, {1,6}, {4,6} };

        // 방문했는지
        boolean[] visit = new boolean[9];

        System.out.println(bfs(1, graph, visit));
        // 예상 결과값 : 1 -> 2 -> 3 -> 7 -> 5 -> 6 -> 4 -> 8 -> 
    }

    static String bfs(int start, int[][] graph, boolean[] visit) {
        StringBuilder sb = new StringBuilder();

        Queue<Integer> queue = new LinkedList<Integer>();

        queue.offer(start);

        visit[start] = true;

        while (!queue.isEmpty()) {
            int node = queue.poll();
            sb.append(node + " -> ");
            // 큐에서 꺼낸 노드와 연결된 간선 체크
            for (int i = 0; i < graph[node].length; i++) {
                int temp = graph[node][i];
                // 방문하지 않았으면 방문처리 후에 큐에 삽입
                if (!visit[temp]) {
                    visit   [temp] = true;
                    queue.offer(temp);
                }
            }
        }
        return sb.toString();
    }
}
```

<br> 
<br> 
<br>

**참고 URL : <https://velog.io/@ygy0102/Java-BFS-%EB%84%88%EB%B9%84-%EC%9A%B0%EC%84%A0-%ED%83%90%EC%83%89-%EA%B5%AC%ED%98%84-%EC%9E%90%EB%B0%94-Java>**
