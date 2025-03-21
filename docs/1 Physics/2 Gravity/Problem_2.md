# Problem 2
# Escape Velocities and Cosmic Velocities

## Introduction

In the field of celestial mechanics, the concept of escape velocity is crucial for understanding the conditions required to leave a celestial body's gravitational influence. The escape velocity is the minimum velocity an object must have in order to break free from the gravitational pull of a planet or star.

There are also three important cosmic velocities:
1. **First Cosmic Velocity**: The velocity required for a body to enter a stable orbit around a celestial body.
2. **Second Cosmic Velocity (Escape Velocity)**: The velocity needed to escape the gravitational pull of a celestial body.
3. **Third Cosmic Velocity**: The velocity required to escape the gravitational influence of a star system, such as the Solar System.

These concepts are foundational in space exploration, from launching satellites to interplanetary missions.

## Definitions of Cosmic Velocities

### 1. First Cosmic Velocity

The **first cosmic velocity** is the orbital velocity required for an object to move in a stable, circular orbit around a celestial body. This velocity can be derived from the balance between the gravitational force and the centripetal force that keeps the object in orbit.

The formula for the first cosmic velocity \(v_1\) is:

$$
v_1 = \sqrt{\frac{GM}{r}}
$$

Where:
- \(G\) is the gravitational constant \((6.67430 \times 10^{-11} \, \text{m}^3 \text{kg}^{-1} \text{s}^{-2})\),
- \(M\) is the mass of the central body (e.g., Earth, Mars, Jupiter),
- \(r\) is the radius of the orbit (distance from the center of the celestial body to the object in orbit).

### 2. Second Cosmic Velocity (Escape Velocity)

The **second cosmic velocity** is the escape velocity. It is the minimum velocity needed to escape the gravitational influence of a celestial body without further propulsion. The escape velocity \(v_e\) is given by:

$$
v_e = \sqrt{\frac{2GM}{r}}
$$

Where:
- \(G\) is the gravitational constant,
- \(M\) is the mass of the celestial body,
- \(r\) is the distance from the center of the body to the point of escape.

### 3. Third Cosmic Velocity

The **third cosmic velocity** is the velocity required to escape the gravitational influence of a star system, such as the Solar System. This velocity depends on the mass of the central star and the distance from the star. The third cosmic velocity \(v_3\) is given by:

$$
v_3 = \sqrt{\frac{2GM_{\text{star}}}{r_{\text{star}}}}
$$

Where:
- \(G\) is the gravitational constant,
- \(M_{\text{star}}\) is the mass of the central star (e.g., the Sun),
- \(r_{\text{star}}\) is the distance from the star at which the object is located.

## Parameters Affecting These Velocities

- **Mass of the Celestial Body**: The greater the mass of the celestial body, the higher the required velocity for orbiting or escaping.
- **Radius of the Celestial Body**: The closer the object is to the center of the celestial body (or the star), the higher the required velocity.
- **Distance from the Star**: For the third cosmic velocity, the distance from the central star influences the escape velocity from the star system.

## Python Implementation

### Code to Calculate and Visualize Cosmic Velocities

The following Python code calculates and visualizes the first, second, and third cosmic velocities for different celestial bodies such as Earth, Mars, and Jupiter.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant in m^3 kg^-1 s^-2

# Masses (kg) and radii (m) for Earth, Mars, Jupiter, and the Sun
bodies = {
    'Earth': {'mass': 5.972e24, 'radius': 6.371e6},
    'Mars': {'mass': 0.64171e24, 'radius': 3.396e6},
    'Jupiter': {'mass': 1.898e27, 'radius': 6.991e7},
    'Sun': {'mass': 1.989e30, 'radius': 6.9634e8},
}

# Function to calculate the first cosmic velocity
def first_cosmic_velocity(mass, radius):
    return np.sqrt(G * mass / radius)

# Function to calculate the second cosmic velocity (escape velocity)
def second_cosmic_velocity(mass, radius):
    return np.sqrt(2 * G * mass / radius)

# Function to calculate the third cosmic velocity (escape velocity from star system)
def third_cosmic_velocity(mass_star, radius_star):
    return np.sqrt(2 * G * mass_star / radius_star)

# Calculate velocities for each body
velocities = {}
for body, params in bodies.items():
    if body != 'Sun':
        v1 = first_cosmic_velocity(params['mass'], params['radius'])
        v2 = second_cosmic_velocity(params['mass'], params['radius'])
        velocities[body] = {'v1': v1, 'v2': v2}
    else:
        # For Sun, calculating third cosmic velocity
        v3 = third_cosmic_velocity(params['mass'], params['radius'])
        velocities[body] = {'v3': v3}

# Plotting the velocities
plt.figure(figsize=(10, 6))
labels = []
v1_vals = []
v2_vals = []
v3_vals = []

# Plot the velocities for Earth, Mars, Jupiter, and Sun
for body, vel in velocities.items():
    if body != 'Sun':
        labels.append(body + ' - First Cosmic Velocity (m/s)')
        v1_vals.append(vel['v1'])
        labels.append(body + ' - Second Cosmic Velocity (m/s)')
        v2_vals.append(vel['v2'])
    else:
        labels.append(body + ' - Third Cosmic Velocity (m/s)')
        v3_vals.append(vel['v3'])

# Combined bar chart for velocities
x = np.arange(len(labels))
velocities_all = v1_vals + v2_vals + v3_vals

plt.bar(x, velocities_all, tick_label=labels)
plt.xlabel('Celestial Bodies and Velocities')
plt.ylabel('Velocity (m/s)')
plt.title('Escape and Cosmic Velocities for Different Celestial Bodies')
plt.xticks(rotation=90)
plt.grid(True)
plt.tight_layout()
plt.show()
.