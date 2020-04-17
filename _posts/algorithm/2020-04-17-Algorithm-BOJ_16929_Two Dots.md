---
layout: post
title:  " BOJ 16929번 Two Dots "
category: Algorithm
tags: [Algorithm]
comments: true
---





```java


import java.util.Scanner;

public class BOJ_16929 {

    static String[][] colors;
    static boolean[][] visited;
    static int[][] dist;
    static int n, m;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] split = sc.nextLine().split("\\s");
        n = Integer.parseInt(split[0]);
        m = Integer.parseInt(split[1]);
        colors = new String[n][m];
        visited = new boolean[n][m];
        dist = new int[n][m];

        for (int i = 0; i < n; i++) {
            char[] line = sc.nextLine().toCharArray();
            for (int j = 0; j < m; j++) {
                colors[i][j] = line[j] + "";
            }
        }
        solve(n, m);
    }

    private static void solve(int n, int m) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (!visited[i][j]){
                    if(dfs(i, j, 0, colors[i][j])){
                        System.out.println("Yes");
                        return;
                    }
                }
            }
        }
        System.out.println("No");

    }

    static int[] goX = new int[]{-1, 1, 0, 0};
    static int[] goY = new int[]{0, 0, -1, 1};

    private static boolean dfs(int x, int y, int count, String color) {
        if (visited[x][y]) {
            if (colors[x][y].equals(color) && (count - dist[x][y]) >= 4) {
                return true;
            } else
                return false;
        }

        visited[x][y] = true;
        dist[x][y] = count;

        for (int i = 0; i < 4; i++) {
            int nextX = x + goX[i];
            int nextY = y + goY[i];

            if (nextX >= 0 && nextX < n && nextY >= 0 && nextY < m) {
                if (color.equals(colors[nextX][nextY])) {
                    if(dfs(nextX, nextY, count + 1, color))
                        return true;
                }
            }
        }
        return false;
    }
}

```

