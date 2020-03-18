---
layout: post
title:  "BOJ 1260번 DFS와 BFS" 
category: Algorithm
tags: [Algorithm]
comments: true
---



```java

import java.util.*;

public class BOJ_1260 {

    static boolean[] check;
    static ArrayList<Integer>[] list;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int start = sc.nextInt();

        list = new ArrayList[n + 1];
        check = new boolean[n + 1];
        for (int i = 1; i <= n; i++) {
            list[i] = new ArrayList<>();
        }

        for (int i = 1; i <= m; i++) {
            int from = sc.nextInt();
            int to = sc.nextInt();
            list[from].add(to);
            list[to].add(from);
        }

        for (int i = 1; i <= n; i++) {
            Collections.sort(list[i]);
        }

        dfs(start);
        System.out.println();
        Arrays.fill(check, false);
        bfs(start);
        System.out.println();

    }

    private static void dfs(int u) {

        if (check[u])
            return;

        check[u] = true;

        System.out.print(u + " ");

        for (int v : list[u]) {
            if (!check[v])
                dfs(v);
        }
    }

    private static void bfs(int u) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(u);
        check[u] = true;
        while (!queue.isEmpty()) {
            int v = queue.remove();
            System.out.print(v + " ");
            for (int adj : list[v]) {
                if (!check[adj]) {
                    check[adj] = true;
                    queue.add(adj);
                }
            }
        }
    }

}

```





