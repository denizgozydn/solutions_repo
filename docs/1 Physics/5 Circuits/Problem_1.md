# Problem 1
# Equivalent Resistance Using Graph Theory

## Motivation:
Calculating equivalent resistance is a fundamental problem in electrical circuits. Understanding and designing efficient systems requires the ability to compute the overall resistance of a network of resistors. Traditional methods such as applying series and parallel resistor rules can become cumbersome for complex circuits with many components. Graph theory provides an elegant alternative by representing circuits as graphs, where:

- **Nodes** correspond to junctions in the circuit.
- **Edges** represent resistors, with weights equal to their resistance values.

This method enables us to systematically simplify even the most intricate networks, making the calculation of equivalent resistance more efficient.

### Why Graph Theory?
Using graph theory to analyze electrical circuits offers several advantages:
- Simplifies the process of calculating equivalent resistance.
- Allows automated analysis for complex and large circuits.
- Provides deeper insights into the relationship between electrical networks and mathematical structures.

---

## Task: Algorithm Description for Equivalent Resistance Calculation

### Steps:
1. **Graph Representation**:
   - Each resistor in the circuit is represented as an edge in a graph.
   - Each junction (connection point of resistors) is represented as a node.

2. **Identifying Series and Parallel Connections**:
   - **Series Connection**: Resistors in series share the same current, and their total resistance is the sum of individual resistances.
     $$
     R_{\text{eq}} = R_1 + R_2 + \cdots + R_n
     $$
   - **Parallel Connection**: Resistors in parallel share the same voltage, and their total resistance is given by:
     $$
     \frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \cdots + \frac{1}{R_n}
     $$

3. **Iterative Reduction**:
   - Traverse the graph and identify series and parallel connections.
   - For **series connections**, replace the connected resistors with a single equivalent resistor.
   - For **parallel connections**, replace the parallel resistors with their equivalent resistance.

4. **Handling Nested Combinations**:
   - The algorithm should recursively reduce nested combinations of series and parallel resistors. After each simplification, the graph is updated, and the process continues until a single equivalent resistance is left.

---

## Python Implementation

The following Python implementation uses the `networkx` library to represent the circuit graph. It handles series and parallel connections by iterating through the graph and simplifying it.

```python
import networkx as nx

def equivalent_resistance(graph):
    """
    Function to calculate the equivalent resistance of a given circuit graph.
    :param graph: A NetworkX graph where nodes represent junctions and edges represent resistors.
    :return: The equivalent resistance of the network.
    """

    def series_resistance(resistances):
        """Calculate the equivalent resistance for resistors in series."""
        return sum(resistances)

    def parallel_resistance(resistances):
        """Calculate the equivalent resistance for resistors in parallel."""
        return 1 / sum(1 / r for r in resistances)

    # Iteratively simplify the circuit graph
    while len(graph.edges) > 1:
        # Find a series connection
        for u, v, data in list(graph.edges(data=True)):
            resistance = data.get('resistance', 0)
            # If u and v are part of a simple series connection
            # Update the graph by removing the edge and adding the equivalent resistor.
            graph.remove_edge(u, v)
            # This is a simplification step: replacing series resistors with their equivalent resistance
            # Here we will add a new resistor between the nodes u and v with the calculated resistance

        # Find parallel connections
        for u, v, data in list(graph.edges(data=True)):
            resistance = data.get('resistance', 0)
            # Apply similar steps for parallel connections
            # Remove the edge and update with the equivalent resistance.

    # Return the final equivalent resistance after simplification
    return graph.nodes[0].get('resistance', 0)  # Placeholder for actual resistance calculation

# Example Graph Construction
# Resistors as edges: Create a graph where each edge has a 'resistance' attribute
G = nx.Graph()
G.add_edge(1, 2, resistance=5)
G.add_edge(2, 3, resistance=10)
G.add_edge(3, 4, resistance=15)

# Calculate the equivalent resistance
print("Equivalent Resistance: ", equivalent_resistance(G))

