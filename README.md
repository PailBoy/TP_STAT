# This is the TP for the Statistcs by IMAHO Aladin, HADJ SASSI Mahdi



print("Analysis of the Markov Chain:")
counts = {0: markov_chain.count(0), 1: markov_chain.count(1), 2: markov_chain.count(2)}
for state, count in counts.items():
    print(f"State {state}: {count} occurrences")

# Visualization
plt.bar(counts.keys(), counts.values(), tick_label=["Rock", "Paper", "Scissors"])
plt.title("State Distribution in the Generated Markov Chain")
plt.xlabel("States")
plt.ylabel("Frequency")
plt.show()