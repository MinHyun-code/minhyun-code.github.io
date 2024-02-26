---
layout: post
title: "Dijkstra - 최단경로"
subtitle: "Dijkstra"
category: "algorithm"
date: 2024-02-26
background: '/img/posts/codeImg.jpg'
---

# 다익스트라

`그래프 최단 경로 알고리즘` 

`하나의 정점에서 출발하는 최단 거리` 

`음수 가중치 X`

<br>
<br>

> 백준 문제 참고 https://www.acmicpc.net/problem/5972

## 인접행렬방식
`시간 복잡도 : O(N^2)`

```java
public class Main {

	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static StringBuilder sb = new StringBuilder();
	
	static int N, M;
	static int[][] arr;
	static int[] distance;
	
	public static void main(String[] args) throws IOException{
	
		st = new StringTokenizer(br.readLine());
		
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());

		arr = new int[N+1][N+1];

		for(int i=0; i<=N; i++) {
			for(int j=0; j<=N; j++) {
				arr[i][j] = 1001;          // 최대 값으로 셋팅
			}
		}
		
		for(int i=0; i<M; i++) {
			st = new StringTokenizer(br.readLine());

			int A_i = Integer.parseInt(st.nextToken());
			int B_i = Integer.parseInt(st.nextToken());
			int C_i = Integer.parseInt(st.nextToken());

			arr[A_i][B_i] = C_i;          // 양방향
			arr[B_i][A_i] = C_i;
		}
		
		Dijkstra(1);
		
		System.out.println(distance[N]);
	}
	
	private static void Dijkstra(int node) {
		
		distance = new int[N+1];			// 최단 거리를 저장할 변수
		boolean[] visited = new boolean[N+1];	// 해당 노드를 방문했는지 체크할 변수
		
		for(int i=1; i<=N; i++) {
			distance[i] = Integer.MAX_VALUE;
		}
		
		// 시작 노드 값 설정
		distance[node] = 0;
		visited[node] = true;
		
		
		// 연결 노드 distance 셋팅
		for(int i=0; i<N; i++) {
			if(!visited[i] && arr[node][i] != Integer.MAX_VALUE) {
				distance[i] = arr[node][i];
			}
		}
		
		for(int i=1; i<N; i++) {         // 시작점 셋팅 하였으므로 1개 제외
			int min = Integer.MAX_VALUE;
			int min_index = i;
			
			for(int j=1; j<=N; j++) {
				
				if(!visited[j]) {
 					if(distance[j] < min) {
 						min = distance[j];
 						min_index = j;
 					}
				}
			}
			
			// 다른 노드를 거쳐서 가는 비용이 적은지 확인
			
			visited[min_index] = true;
			
			for(int j=1; j<=N; j++) {
				if(!visited[j] && arr[min_index][j] != Integer.MAX_VALUE) {
					if(distance[min_index] + arr[min_index][j] < distance[j]) {
						distance[j] = distance[min_index] + arr[min_index][j];
					}
				}
			}
		}
	}
}
```

<br>
<br>

## 우선순위 큐 방식 (연결리스트 사용)
`시간 복잡도 : O(ElogN)`

```java
class Node implements Comparable<Node> {

	int index;
	int weight;
	
	public Node(int index, int weight) {
		this.index = index;
		this.weight = weight;
	}
	
	@Override
	public int compareTo(Node o) {
		return Integer.compare(this.weight, o.weight);
	}
}

public class Main {

	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
	static StringTokenizer st;
	static StringBuilder sb = new StringBuilder();
	
	static int N, M;
	static List<List<Node>> graph = new ArrayList<List<Node>>();
	
	public static void main(String[] args) throws IOException{
	
		st = new StringTokenizer(br.readLine());
		
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());

		for(int i=0; i<N; i++) {
			graph.add(new ArrayList<Node>());
		}
		
		for(int i=0; i<M; i++) {
			st = new StringTokenizer(br.readLine());

			int start = Integer.parseInt(st.nextToken())-1;
			int end = Integer.parseInt(st.nextToken())-1;
			int weight = Integer.parseInt(st.nextToken());
			
			graph.get(start).add(new Node(end, weight));
			graph.get(end).add(new Node(start, weight));
		}
		
		Dijkstra(0);
	}
	
	private static void Dijkstra(int index) {
		PriorityQueue<Node> pq = new PriorityQueue<Node>();
		int[] distance = new int[N];
		
		Arrays.fill(distance, Integer.MAX_VALUE);
		
		distance[index] = 0;
		pq.offer(new Node(index, 0));
		
		while(!pq.isEmpty()) {
			Node node = pq.poll();
			int nodeIndex = node.index;
			int weight = node.weight;
		
		/* 
		 * 큐는 최단거리 기준 오름차순 정렬 
		 */
		
			if(weight > distance[nodeIndex]) {
				continue;
			}
			
			for(Node linkedNode : graph.get(nodeIndex)) {
				if(weight + linkedNode.weight < distance[linkedNode.index]) {
					
					distance[linkedNode.index] = weight + linkedNode.weight;
					
					pq.offer(new Node(linkedNode.index, distance[linkedNode.index]));
				}
			}
		}
		
		System.out.println(distance[N-1]);
	}
}
```

<br> 
<br> 
<br>
