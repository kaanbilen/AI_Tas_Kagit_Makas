import random
from collections import Counter

def get_ai_choice(history):
    if not history:
        return random.choice(["taş", "kağıt", "makas"])
    
    most_common = Counter(history).most_common(1)[0][0]
    
    counter_moves = {
        "taş": "kağıt",  # Taş oynama eğiliminde ise AI kağıt oynar
        "kağıt": "makas", # Kağıt oynama eğiliminde ise AI makas oynar
        "makas": "taş"     # Makas oynama eğiliminde ise AI taş oynar
    }
    
    return counter_moves[most_common]

def determine_winner(player, ai):
    if player == ai:
        return "Berabere!"
    elif (player == "taş" and ai == "makas") or \
         (player == "kağıt" and ai == "taş") or \
         (player == "makas" and ai == "kağıt"):
        return "Tebrikler, kazandınız!"
    else:
        return "AI kazandı!"

def main():
    print("Taş-Kağıt-Makas oyununa hoş geldiniz! Çıkmak için 'çık' yazabilirsiniz.")
    history = []
    
    while True:
        player_choice = input("Taş, Kağıt, Makas seçin: ").lower()
        if player_choice == "çık":
            break
        if player_choice not in ["taş", "kağıt", "makas"]:
            print("Geçersiz giriş, lütfen taş, kağıt veya makas seçin!")
            continue
        
        ai_choice = get_ai_choice(history)
        print(f"AI'nin seçimi: {ai_choice}")
        
        result = determine_winner(player_choice, ai_choice)
        print(result)
        
        history.append(player_choice)
        print("---")
    
    print("Oyun bitti! Teşekkürler.")

if __name__ == "__main__":
    main()
