class Solution:
    def __init__(self, circuit):
        self.circuit = circuit

    def do_power_flow(self):
        # Extract circuit components
        Va = self.circuit['voltage_source']  # Voltage at bus A
        Rab = self.circuit['resistor']      # Resistance between A and B
        P_load = self.circuit['load_power'] # Load power at bus B
        Vb = self.circuit['load_voltage']  # Nominal voltage of the load

        # Calculate equivalent impedance of the load (constant impedance model)
        Z_load = (Vb ** 2) / P_load

        # Calculate total equivalent impedance
        Z_eq = Rab + Z_load

        # Calculate circuit current
        I = Va / Z_eq

        # Calculate bus B voltage
        Vb = Va - I * Rab

        # Store results in the circuit dictionary
        self.circuit['bus_A_voltage'] = Va
        self.circuit['bus_B_voltage'] = Vb
        self.circuit['circuit_current'] = I

    def display_results(self):
        print(f"bus A voltage = {self.circuit['bus_A_voltage']} V")
        print(f"bus B voltage = {self.circuit['bus_B_voltage']} V")
        print(f"Circuit current = {self.circuit['circuit_current']} A")


from Solution import Solution

# Define the circuit components
circuit = {
    'voltage_source': 100.0,  # Voltage at bus A (V)
    'resistor': 5.0,          # Resistor between buses A and B (Ohms)
    'load_power': 2000.0,     # Load power (W)
    'load_voltage': 100.0     # Nominal load voltage (V)
}

# Create a Solution object
solution = Solution(circuit)

# Perform power flow calculation
solution.do_power_flow()

# Display results
solution.display_results()
