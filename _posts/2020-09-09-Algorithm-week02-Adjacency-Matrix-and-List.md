---
layout: post
title: "[알고리즘] Adjacency Matrix and List"
date: 2020-09-09 00:00:00
categories: [SOPHOMORE]
tags: [ALGORITHM]
last_modified_at: 2020-09-09
---

[lab02](https://github.com/Sinyoung3016/Fortune_In_Sophomore/tree/master/AL02_Java/AL02)


<figure>
<center><img src="/Fortune/assets/sophomore/Algorithm/lec02.jpg" alt="Midnight" style="width:100%"></center>
</figure>

```{.java}
    public class Graph {

        private static int numOfVertex;
        private static int numOfEdge;
        public static Scanner input = new Scanner(System.in);

        public Graph(int numOfVertex, int numOfEdge){
            this.numOfVertex = numOfVertex;
            this.numOfEdge = numOfEdge;
        }

        public static int[][] adjacencyMatrix() {
            int[][] vertex = new int[numOfVertex][numOfVertex];
            for (int i = 0; i < numOfVertex; i++)
                vertex[input.nextInt()][input.nextInt()] = 1;
            return vertex;
        }

        public static ArrayList[] adjacencyList() {
            ArrayList<Integer> [] head = new ArrayList[numOfVertex];
            for (int i = 0; i < numOfVertex; i++)
                head[i] = new ArrayList<>();

            for (int i = 0; i < numOfEdge; i++)
                head[input.nextInt()].add(input.nextInt());

            return head;
        }

        public static Node[] adjacencyMultiList() {
            Node [] head = new Node[numOfVertex];
            Node [] link = new Node[numOfVertex +1]; //link[numOfVertex] = null;
            for (int p = 0; p < numOfVertex; p++)
                link[p] = new Node(input.nextInt(), input.nextInt());

            for (int p = 0; p < numOfVertex; p++){
                link[p].i_link = link[input.nextInt()];
                link[p].j_link = link[input.nextInt()];
            }

            for (int p = 0; p < numOfVertex; p++) {
                head[p] = link[input.nextInt()];
            }
            return head;
        }

        private static class Node{
            public boolean mark;
            public int i, j;
            public Node i_link, j_link;

            public Node(int i, int j){
                this.i = i;
                this.j = j;
            }
        }
    }

```

<br>
<br>



