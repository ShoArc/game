# game
from time import sleep, time
import threading

flashlight_on = False
flashlight_timer = 0
FLASHLIGHT_MAX_TIME = 120  # 120 seconds

def print_slow(txt, delay=0.1):
    for x in txt:
        print(x, end='', flush=True)
        sleep(delay)
    print()

def start_flashlight_timer():
    global flashlight_timer
    start_time = time()
    elapsed = 0
    while elapsed < FLASHLIGHT_MAX_TIME and flashlight_on:
        elapsed = time() - start_time
        sleep(1)
    if flashlight_on:
        print("\nFlashlight has run out of battery!")
        turn_off_flashlight()

def turn_on_flashlight():
    global flashlight_on, flashlight_timer
    if not flashlight_on:
        flashlight_on = True
        flashlight_timer = 0
        print("\nFlashlight is on.")
        threading.Thread(target=start_flashlight_timer).start()

def turn_off_flashlight():
    global flashlight_on, flashlight_timer
    if flashlight_on:
        flashlight_on = False
        print("\nFlashlight is off.")
        flashlight_timer = 0

def reload_flashlight():
    global flashlight_timer
    flashlight_timer = 0
    print("\nFlashlight battery reloaded.")

def option_1():
    print_slow("You walk around and find nothing.")
    print_slow("Just an empty space... No car, no people... Just you and the sound of dripping water.")
    sleep(1)
    print_slow("You see a dim yellow light flickering far away.")
    print("1. Go towards the light.")
    print("2. Walk around more away from the light.")
    print("Press 'f' to toggle flashlight (if available).")

    choice = input("Enter your choice (1, 2, or f): ")
    if choice == '1':
        option_1a()
    elif choice == '2':
        option_1b()
    elif choice.lower() == 'f':
        if flashlight_on:
            turn_off_flashlight()
        else:
            turn_on_flashlight()
    else:
        print("Invalid choice. Please enter either 1, 2, or f.")

def option_1a():
    print_slow("You slowly walk towards the light and you hear a distant static voice.")
    print_slow("You reach the light and listen closely... The voice... The voice is coming from the door under that yellow flickering light.")
    print("1. Go inside the room.")
    print("2. Turn around and look for a different path.")
    print("Press 'f' to toggle flashlight (if available).")

    choice = input("Enter your choice (1, 2, or f): ")
    if choice == '1':
        option_1aa()
    elif choice.lower() == 'f':
        if flashlight_on:
            turn_off_flashlight()
        else:
            turn_on_flashlight()
    else:
        print("Invalid choice. Please enter either 1, 2, or f.")

def option_1aa():
    print_slow("You walk in and find a table on which a red light is blinking.")
    print_slow("Your eyes adjust to the dark and you see a radio and a torch and 2 batteries.")
    print("1. Pick the radio and the flashlight.")
    print("Press 'f' to toggle flashlight (if available).")

    choice = input("Enter your choice (1 or f): ")
    if choice == '1':
        # Implement picking up radio and flashlight
        print("You picked up the radio and flashlight.")
    elif choice.lower() == 'f':
        if flashlight_on:
            turn_off_flashlight()
        else:
            turn_on_flashlight()
    else:
        print("Invalid choice. Please enter either 1 or f.")

def option_1ab():
    print_slow("You decide to walk around more in the dark...")
    # Add more storyline here if needed

def option_2():
    print_slow("You sit down and gather your thoughts.")
    print_slow("Trying to remember how you got here...")
    print("1. Walk Around")
    print("Press 'f' to toggle flashlight (if available).")

    choice = input("Enter (1 or f): ")
    if choice == '1':
        option_1()
    elif choice.lower() == 'f':
        if flashlight_on:
            turn_off_flashlight()
        else:
            turn_on_flashlight()
    else:
        print("Invalid choice. Please enter either 1 or f.")

print_slow("You are trapped alone in a basement of a parking lot.")
sleep(1)
print_slow("You look around and you don't remember anything.")
sleep(2)
print_slow("You get up and look around and you get a gut feeling that something ain't right.")
print("1. Walk Around.")
print("2. Stay where you are.")
print("Press 'f' to toggle flashlight (if available).")

choice = input("Enter your choice (1, 2, or f): ")

# Check user's choice and execute corresponding function
if choice == '1':
    option_1()
elif choice == '2':
    option_2()
elif choice.lower() == 'f':
    if flashlight_on:
        turn_off_flashlight()
    else:
        turn_on_flashlight()
else:
    print("Invalid choice. Please enter either 1, 2, or f.")
