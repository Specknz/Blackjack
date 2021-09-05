import random
from os import system
from art import logo


def yes_no_prompt(message, yes_return, no_return):
    while True:
        try:
            user_input = str(input(message).lower())
            if user_input == 'y':
                return yes_return
            elif user_input == 'n':
                return no_return
            else:
                print('Please enter y or n')
        except:
            print('Please enter y or n')


def get_cards():
    return [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]


def deal_hand():
    cards = get_cards()
    return [random.choice(cards) for i in range(2)]


def calculate_hand(hand):
    if sum(hand) == 21 and len(hand) == 2:
        return -1
    else:
        return sum(hand)


def hand_list_to_string(hand):
    return ''.join(str(card) + ', ' for card in hand).strip(', ')


def check_for_ace(hand):
    for i in range(len(hand)):
        if hand[i] == 11:
            hand[i] = 1
            print('Ace switched to 1 otherwise you would bust!')
            break
    return hand
    

def print_hand_amount(hand, hand_owner):
    print(f'{hand_owner} has a hand of: {sum(hand)}')


def bust_player_hand(player_hand):
    player_total = calculate_hand(player_hand)
    system('cls')
    print('\nYou are bust! You\'ve gone over 21')
    print(f'Your hand: {hand_list_to_string(player_hand)} (Total: {player_total})')


def determine_outcome(house_hand, player_hand):
    system('cls')
    player_total = calculate_hand(player_hand)
    house_total = calculate_hand(house_hand)
    # Lose
    if house_total > player_total and house_total <= 21 and player_total != 0 and player_total < 21:
        print(f'\nYou have lost the hand\n')
        print(f'Houses hand: {hand_list_to_string(house_hand)} (Total: {house_total})')
        print(f'Your hand: {hand_list_to_string(player_hand)} (Total: {player_total})')
    # Draw
    elif house_total == player_total:
        print(f'\nYou draw.')
        print(f'Houses hand: {hand_list_to_string(house_hand)} (Total: {house_total})')
        print(f'Your hand: {hand_list_to_string(player_hand)} (Total: {player_total})')
    # House blackjack
    elif house_hand == -1:
        print(f'\nYou have lost the hand\n')
        print(f'The house has a Blackjack!\n')
        print(f'Houses hand: {hand_list_to_string(house_hand)} (Total: {house_total})')
    # Player blackjack
    elif player_total == -1:
        print(f'\nYou have won!')
        print(f'You have a Blackjack!')
        print(f'Your hand: {hand_list_to_string(player_hand)} (Total: 21)')
    # Win
    else:
        print(f'\nYou have won!')
        print(f'Houses hand: {hand_list_to_string(house_hand)} (Total: {house_total})')
        print(f'Your hand: {hand_list_to_string(player_hand)} (Total: {player_total})')


def hit_hand(hand):
    cards = get_cards()
    return hand.append(random.choice(cards))


def hit_or_stand():
    return yes_no_prompt('\nWould you like to hit?: (y, n) ', True, False)


def restart_game():
    yes_no_prompt('\nWould you like to play again?: (y, n) ', game, exit)()


def start_game():
    print(logo)
    yes_no_prompt('\nWould you like to play?: (y, n) ', game, exit)()


# Game loop
def game():
    system('cls')
    player_hand = deal_hand()
    house_hand = deal_hand()
    while True:
        print(f'\nThe house cards: {house_hand[0]}, ?')
        print(f'Your cards: {hand_list_to_string(player_hand)} (Total: {sum(player_hand)})')
        # Check if player Blackjack
        if calculate_hand(player_hand) == -1:
            break
        # Check if player bust
        if calculate_hand(player_hand) > 21:
            # Switch 11 to 1 if player bust
            player_hand = check_for_ace(player_hand)
            # Recheck if player bust
            if calculate_hand(player_hand) > 21:
                bust_player_hand(player_hand)
                break
            else:
                continue
        # Player hit or Stand
        if hit_or_stand():
            hit_hand(player_hand)
            continue
        # House hit or stand
        else:
            while True:
                if calculate_hand(house_hand) == 0:
                    break
                elif calculate_hand(house_hand) < 17:
                    hit_hand(house_hand)
                    print(f'House chose to hit.\nHouses new hand: {house_hand}')
                    continue
                else:
                    break
        determine_outcome(house_hand, player_hand)
        break
        # Finish game


# Prompt to start game
start_game()

while True:
    restart_game()
