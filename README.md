FUNCTION createGraph():
    PRINT "Enter number of locations: "
    READ n
    PRINT "Enter adjacency matrix (enter 0 for no direct path):"
    FOR i = 0 TO n-1:
        FOR j = 0 TO n-1:
            READ graph[i][j]
            IF graph[i][j] == 0 AND i != j:
                graph[i][j] = INT_MAX // No direct path

FUNCTION dijkstra(start):
    DECLARE distance[MAX], visited[MAX], parent[MAX]
    FOR i = 0 TO n-1:
        distance[i] = INT_MAX
        visited[i] = 0
        parent[i] = -1
    distance[start] = 0

    FOR count = 0 TO n-2:
        min = INT_MAX
        FOR v = 0 TO n-1:
            IF visited[v] == 0 AND distance[v] < min:
                min = distance[v]
                min_index = v
        visited[min_index] = 1
        FOR v = 0 TO n-1:
            IF visited[v] == 0 AND graph[min_index][v] != INT_MAX AND 
               distance[min_index] + graph[min_index][v] < distance[v]:
                distance[v] = distance[min_index] + graph[min_index][v]
                parent[v] = min_index

    PRINT "Shortest paths from location", start, ":"
    FOR i = 0 TO n-1:
        IF i != start:
            PRINT "To", i, ": Distance =", distance[i]

FUNCTION main():
    createGraph()
    PRINT "Enter starting location: "
    READ start
    dijkstra(start)
    RETURN 0
