# This is the TP for the Statistcs by IMAHO Aladin, HADJ SASSI Mahdi



import tkinter as tk

# Step 1: Play function for random strategy
def Play(a):
    """
    Simulates a round of Rock-Paper-Scissors against a computer playing randomly.

    Parameters:
        a (int): Human player's move (0: Rock, 1: Paper, 2: Scissors).

    Returns:
        str: Result of the round (Win, Lose, Draw).
    """
    computer_move = np.random.choice([0, 1, 2])  # Computer plays uniformly randomly
    result_matrix = [["Draw", "Lose", "Win"], ["Win", "Draw", "Lose"], ["Lose", "Win", "Draw"]]
    return result_matrix[a][computer_move]

# Step 2: Create a simple GUI for the game
def start_game():
    def play_round(player_move):
        result = Play(player_move)
        label_result.config(text=f"You: {['Rock', 'Paper', 'Scissors'][player_move]}\nComputer: {['Rock', 'Paper', 'Scissors'][np.random.choice([0, 1, 2])]}\nResult: {result}")

    # Initialize GUI
    root = tk.Tk()
    root.title("Rock-Paper-Scissors Game")

    # Buttons for moves
    tk.Button(root, text="Rock", command=lambda: play_round(0)).grid(row=0, column=0)
    tk.Button(root, text="Paper", command=lambda: play_round(1)).grid(row=0, column=1)
    tk.Button(root, text="Scissors", command=lambda: play_round(2)).grid(row=0, column=2)

    # Result label
    label_result = tk.Label(root, text="Make your move!", font=("Helvetica", 14))
    label_result.grid(row=1, column=0, columnspan=3)

    root.mainloop()

# Uncomment to start the game
# start_game()

# Step 3: Initialize memory matrix for AI strategy
Mem = np.zeros((3, 3), dtype=int)

# Step 4: Play function for AI strategy
def Play2(a):
    """
    Simulates a round of Rock-Paper-Scissors against an AI using transition probabilities.

    Parameters:
        a (int): Human player's move (0: Rock, 1: Paper, 2: Scissors).

    Returns:
        str: Result of the round (Win, Lose, Draw).
    """
    global Mem
    if a is not None:
        computer_move = np.argmax([Mem[a, 2] - Mem[a, 1], Mem[a, 0] - Mem[a, 2], Mem[a, 1] - Mem[a, 0]])
        human_move = a
        Mem[human_move, computer_move] += 1  # Update memory matrix
        result_matrix = [["Draw", "Lose", "Win"], ["Win", "Draw", "Lose"], ["Lose", "Win", "Draw"]]
        return result_matrix[human_move][computer_move]

# Example interaction with AI strategy
# result = Play2(0)  # Simulate a round where human plays "Rock"
# print("Result:", result)

# Step 5: Dynamic Memory Display
print("Dynamic Memory Matrix:")
print(Mem)
