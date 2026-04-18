# MIDTERM
# --- HERO ROSTER (hardcoded) ---
heroes = ["Layla", "Tigreal", "Gusion", "Kagura", "Chou"]
roles = ["Marksman", "Tank", "Assassin", "Mage", "Fighter"]

# --- PLAYER INFO ---
ign = input("In-game name (IGN): ")
rank = input("Current rank: ")

print("\n==========================================")
print("MOBILE LEGENDS -- HERO ROSTER")
print("==========================================")

i = 0
while i < len(heroes):
    print(f"{i + 1}. {heroes[i]} [{roles[i]}]")
    i += 1

# --- VARIABLES FOR MATCH LOG ---
matches = []
wins = 0
losses = 0

print("==========================================")

match_number = 1
while match_number <= 4:
    print(f"-- MATCH {match_number} --")
    hero_num = int(input("Hero number (0 to skip): "))

    if hero_num == 0:
        print("")  # skip match entry
    elif hero_num >= 1 and hero_num <= 5:
        kills = int(input("Kills: "))
        deaths = int(input("Deaths: "))
        assists = int(input("Assists: "))
        result = input("Result (W/L): ").upper()

        if deaths == 0:
            deaths = 1  # avoid division by zero

        kda = (kills + assists) / deaths

        # --- PERFORMANCE TAGS ---
        if kda >= 5 and result == "W":
            tag = "DOMINATION!"
        elif kda >= 5 and result == "L":
            tag = "Carried Hard"
        elif kda < 5 and result == "W":
            tag = "Team Effort"
        else:
            tag = "Better Luck Next Game"

        # --- COUNT WINS/LOSSES ---
        if result == "W":
            wins += 1
        elif result == "L":
            losses += 1

        match_data = {
            "hero": heroes[hero_num - 1],
            "kda": kda,
            "result": result,
            "tag": tag
        }
        matches.append(match_data)
    else:
        print("Invalid hero number! Skipping...")

    match_number += 1

# --- POST-GAME SUMMARY ---

# Manually find best match (no max() used)
best_match_index = -1
highest_kda = 0
index = 0
while index < len(matches):
    if matches[index]["kda"] > highest_kda:
        highest_kda = matches[index]["kda"]
        best_match_index = index
    index += 1

# --- WIN RATE ---
if len(matches) > 0:
    win_rate = int((wins / len(matches)) * 100)
else:
    win_rate = 0

# --- OUTPUT LOG ---
print("\n=============================================")
print(f"{ign} -- MATCH LOG ({rank})")
print("=============================================")

j = 0
while j < len(matches):
    print(f"[{j + 1}] {matches[j]['hero']} | KDA: {matches[j]['kda']:.2f} | "
          f"{'WIN' if matches[j]['result'] == 'W' else 'LOSS'} | {matches[j]['tag']}")
    j += 1

print("---------------------------------------------")
print(f"Matches Played : {len(matches)}")
print(f"Wins : {wins} | Losses : {losses}")
print(f"Win Rate : {win_rate}%")

if best_match_index != -1:
    print(f"Best Match : [{best_match_index + 1}] {matches[best_match_index]['hero']} "
          f"(KDA: {matches[best_match_index]['kda']:.2f})")
else:
    print("Best Match : None")

print("=============================================")
