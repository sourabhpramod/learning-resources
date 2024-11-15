```c

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <stdbool.h>

struct Node {
    int vertex;
    int weight;
    struct Node* next;
};

struct Graph {
    int numVertices;
    struct Node** adjLists;
    int* visited;
};

struct Node* createNode(int vertex, int weight) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->vertex = vertex;
    newNode->weight = weight;
    newNode->next = NULL;
    return newNode;
}

struct Graph* createGraph(int vertices) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->numVertices = vertices;
    graph->adjLists = (struct Node**)malloc(vertices * sizeof(struct Node*));
    graph->visited = (int*)malloc(vertices * sizeof(int));

    for (int i = 0; i < vertices; i++) {
        graph->adjLists[i] = NULL;
        graph->visited[i] = 0;
    }
    return graph;
}

// Directed edge from src to dest
void addEdge(struct Graph* graph, int src, int dest, int weight) {
    struct Node* newNode = createNode(dest, weight);
    newNode->next = graph->adjLists[src];
    graph->adjLists[src] = newNode;
}

// Breadth-First Search (BFS)
#define MAX_QUEUE_SIZE 100

struct Queue {
    int items[MAX_QUEUE_SIZE];
    int front, rear;
};

struct Queue* createQueue() {
    struct Queue* queue = (struct Queue*)malloc(sizeof(struct Queue));
    queue->front = -1;
    queue->rear = -1;
    return queue;
}

bool isEmpty(struct Queue* queue) {
    return queue->rear == -1;
}

void enqueue(struct Queue* queue, int value) {
    if (queue->rear == MAX_QUEUE_SIZE - 1) return;
    if (queue->front == -1) queue->front = 0;
    queue->items[++queue->rear] = value;
}

int dequeue(struct Queue* queue) {
    if (isEmpty(queue)) return -1;
    int item = queue->items[queue->front++];
    if (queue->front > queue->rear) queue->front = queue->rear = -1;
    return item;
}

void bfs(struct Graph* graph, int startVertex) {
    struct Queue* queue = createQueue();
    graph->visited[startVertex] = 1;
    enqueue(queue, startVertex);

    while (!isEmpty(queue)) {
        int currentVertex = dequeue(queue);
        printf("Visited %d\n", currentVertex);

        struct Node* temp = graph->adjLists[currentVertex];
        while (temp) {
            int adjVertex = temp->vertex;
            if (!graph->visited[adjVertex]) {
                graph->visited[adjVertex] = 1;
                enqueue(queue, adjVertex);
            }
            temp = temp->next;
        }
    }
}

// Depth-First Search (DFS)
void dfs(struct Graph* graph, int vertex) {
    graph->visited[vertex] = 1;
    printf("Visited %d\n", vertex);

    struct Node* temp = graph->adjLists[vertex];
    while (temp) {
        int adjVertex = temp->vertex;
        if (!graph->visited[adjVertex]) {
            dfs(graph, adjVertex);
        }
        temp = temp->next;
    }
}

// Prim's Algorithm (MST)
int minKey(int key[], int mstSet[], int vertices) {
    int min = INT_MAX, min_index;
    for (int v = 0; v < vertices; v++)
        if (mstSet[v] == 0 && key[v] < min)
            min = key[v], min_index = v;
    return min_index;
}

void primMST(struct Graph* graph) {
    int parent[graph->numVertices];
    int key[graph->numVertices];
    int mstSet[graph->numVertices];

    for (int i = 0; i < graph->numVertices; i++) {
        key[i] = INT_MAX;
        mstSet[i] = 0;
    }

    key[0] = 0;
    parent[0] = -1;

    for (int count = 0; count < graph->numVertices - 1; count++) {
        int u = minKey(key, mstSet, graph->numVertices);
        mstSet[u] = 1;

        struct Node* temp = graph->adjLists[u];
        while (temp) {
            int v = temp->vertex;
            if (!mstSet[v] && temp->weight < key[v]) {
                parent[v] = u;
                key[v] = temp->weight;
            }
            temp = temp->next;
        }
    }

    printf("Edge \tWeight\n");
    for (int i = 1; i < graph->numVertices; i++)
        printf("%d - %d \t%d \n", parent[i], i, key[i]);
}

// Dijkstra's Algorithm
int minDistance(int dist[], int sptSet[], int vertices) {
    int min = INT_MAX, min_index;
    for (int v = 0; v < vertices; v++)
        if (sptSet[v] == 0 && dist[v] <= min)
            min = dist[v], min_index = v;
    return min_index;
}

void dijkstra(struct Graph* graph, int src) {
    int dist[graph->numVertices];
    int sptSet[graph->numVertices];

    for (int i = 0; i < graph->numVertices; i++) {
        dist[i] = INT_MAX;
        sptSet[i] = 0;
    }

    dist[src] = 0;

    for (int count = 0; count < graph->numVertices - 1; count++) {
        int u = minDistance(dist, sptSet, graph->numVertices);
        sptSet[u] = 1;

        struct Node* temp = graph->adjLists[u];
        while (temp) {
            int v = temp->vertex;
            if (!sptSet[v] && dist[u] != INT_MAX && dist[u] + temp->weight < dist[v]) {
                dist[v] = dist[u] + temp->weight;
            }
            temp = temp->next;
        }
    }

    printf("Vertex \tDistance from Source\n");
    for (int i = 0; i < graph->numVertices; i++)
        printf("%d \t\t %d\n", i, dist[i]);
}

int main() {
    int vertices = 5;
    struct Graph* graph = createGraph(vertices);

    addEdge(graph, 0, 1, 2);
    addEdge(graph, 0, 4, 1);
    addEdge(graph, 1, 2, 3);
    addEdge(graph, 1, 3, 8);
    addEdge(graph, 1, 4, 5);
    addEdge(graph, 2, 3, 7);
    addEdge(graph, 3, 4, 4);

    printf("BFS:\n");
    bfs(graph, 0);

    for (int i = 0; i < vertices; i++)
        graph->visited[i] = 0;  // Reset visited for DFS

    printf("\nDFS:\n");
    dfs(graph, 0);

    printf("\nPrim's MST:\n");
    primMST(graph);

    printf("\nDijkstra's Shortest Path from vertex 0:\n");
    dijkstra(graph, 0);

    return 0;
}

```