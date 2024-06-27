from time import sleep, time
import threading

flashlight_on = False
flashlight_timer = 0
FLASHLIGHT_MAX_TIME = 120  # 120 seconds
flashlight_event = threading.Event()

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

def handle_input():
    while True:
        choice = input("Enter your choice (1, 2, or f): ")
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

def option_1():
    print_slow("You walk around and find nothing.")
    print_slow("Just an empty space... No car, no people... Just you and the sound of dripping water.")
    sleep(1)
    print_slow("You see a dim yellow light flickering far away.")
    print("1. Go towards the light.")
    print("2. Walk around more away from the light.")

def option_2():
    print_slow("You sit down and gather your thoughts.")
    print_slow("Trying to remember how you got here...")
    print("1. Walk Around.")

def main():
    print_slow("You are trapped alone in a basement of a parking lot.")
    sleep(1)
    print_slow("You look around and you don't remember anything.")
    sleep(2)
    print_slow("You get up and look around and you get a gut feeling that something ain't right.")
    print("1. Walk Around.")
    print("2. Stay where you are.")

    # Start the input handling thread
    input_thread = threading.Thread(target=handle_input)
    input_thread.start()

    while True:
        choice = input("Enter your choice (1, 2, or f): ")
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

if __name__ == "__main__":
    main()

