# lists
names = ['Pacot', 'Paculba', 'Tongco', 'Digdigan', 'Panio', 'Pactolerin']
accounts = ['1112223334445556', '4242424242424242', '1234567891012131', '1010101010101010', '112233445566', '998877665544']
pins = ['3143', '3132', '2233', '1854', '2355', '1236']
balance = [[0], [1000], [1000], [1000], [1000], [1000]]

# default values
i = 0
active = True
clear = "\n" * 100

# Table templates
menu = ("╠═════╦════════════════╦════════════════╦═════╣\n"
        "║  1  ║ Withdraw cash  ║  Transactions  ║  4  ║\n"
        "╠═════╬════════════════╬════════════════╬═════╣\n"
        "║  2  ║ Check Balance  ║     Log out    ║  5  ║\n"
        "╠═════╬════════════════╬════════════════╬═════╣\n"
        "║  3  ║ Deposit cash   ║                ║     ║\n"
        "╚═════╩════════════════╩════════════════╩═════╝\n"
        "Enter choice: ")
transaction = ("╠═════════════════════════════════════════════════════════╣\n"
               "║        Do you want to make another transaction?         ║\n"
               "║            Enter 1 if YES / Enter 2 if NO:              ║\n"
               "╚═════════════════════════════════════════════════════════╝\n"
               "Enter Choice: ")
complete = ("╔════════════════════════════════════════════════════════════════╗\n"
            "                   Thank you have a nice day       \n"
            "                     Press Enter to exit\n"
            "╚════════════════════════════════════════════════════════════════╝"
            )


def anotherTransaction():
    another_transaction = input(transaction)
    if another_transaction == "2":
        input(complete)
        system()
    else:
        print(clear)


def system(i=i):
    while True:
        print(clear)
        print("╔══════════════════════════════════════════════════════╗")
        print("║                                                      ║")
        print("║            Welcome to Group 2  ATM SYSTEM            ║")
        print("║                                                      ║")
        print("╚══════════════════════════════════════════════════════╝")
        card_number = input("Enter card number: ")
        for key, user in enumerate(accounts, start=1):
            if card_number == user:
                while True:
                    password = input("\bEnter Pin: ")
                    if password == pins[accounts.index(user)]:
                        while True:
                            print(clear)
                            print("╔═════════════════════════════════════════════╗\n"
                                  "║ Welcome ", names[accounts.index(user)], "\b")
                            choice = input(menu)
                            if choice == "1":
                                print(clear)
                                print("╔════════════════════════════════════════════════════════╗")
                                print("║                        Withdraw                        ║")
                                print("║            type cancel to cancel transaction           ║")
                                print("╚════════════════════════════════════════════════════════╝")
                                while True:
                                    withdraw = input("Enter Amount: ")
                                    try:
                                        withdraw = abs(int(withdraw))
                                        if withdraw % 100 != 0:
                                            print("╔═════════════════════════════════════════════════════════╗\n"
                                                  "                This ATM can only dispense                \n"
                                                  "║            100, 200, 500 and 1000 Peso notes            ║\n"
                                                  "╚═════════════════════════════════════════════════════════╝")

                                        elif withdraw <= balance[accounts.index(user)][0]:
                                            balance[accounts.index(user)][0] -= withdraw
                                            print("╔═════════════════════════════════════════════════════════╗\n"
                                                  "║                 Total Amount withdrawn                  ║\n"
                                                  "                         ", withdraw, "\n"
                                                  "         Your remaining balance is:",
                                                  balance[accounts.index(user)][0],
                                                  "Pesos")
                                            balance[key - 1].append(withdraw)
                                            anotherTransaction()
                                            break

                                        else:
                                            print("╔═════════════════════════════════════════════════════════╗\n"
                                                  "   You do not have balance to continue this transaction   \n"
                                                  "╠═════════════════════════════════════════════════════════╣")
                                            anotherTransaction()
                                            break
                                    except:

                                        if withdraw == "cancel":
                                            break
                                        else:
                                            print('Invalid Input')

                            elif choice == "2":
                                print(clear)
                                print("╔═════════════════════════════════════════════════════════╗"
                                      "\n            Your current balance is:", balance[accounts.index(user)][0],
                                      "Pesos")
                                anotherTransaction()

                            elif choice == "3":
                                print(clear)
                                print("╔══════════════════════════════════════════════════════╗")
                                print("║                       Deposit                        ║")
                                print("║            Type cancel to cancel transaction         ║")
                                print("╚══════════════════════════════════════════════════════╝")
                                while True:
                                    deposit = input("Enter Amount: ")
                                    try:
                                        deposit = abs(int(deposit))
                                        if deposit % 100 != 0:
                                            print("╔═════════════════════════════════════════════════════════╗\n"
                                                  "║                This ATM can only Receive                ║\n"
                                                  "║            100, 200, 500 and 1000 Peso notes            ║\n"
                                                  "╚═════════════════════════════════════════════════════════╝")

                                        else:
                                            balance[accounts.index(user)][0] += deposit
                                            print("╔═════════════════════════════════════════════════════════╗\n"
                                                  "║                  Total Amount Receive                   ║\n"
                                                  "                         ", deposit, "\n" 
                                                  "         Your current balance is:",
                                                  balance[accounts.index(user)][0], "Pesos")
                                            deposit += 1
                                            balance[key - 1].append(deposit)
                                            anotherTransaction()
                                            break
                                    except:
                                        if deposit == "cancel":
                                            break
                                        else:
                                            print("Invalid input")

                            elif choice == "4":
                                listchecker = len(balance[accounts.index(user)][1:])
                                if listchecker == 0:
                                    print(clear)
                                    print("╔═════════════════════════════════════════════════════════╗\n"
                                          "                    No transaction yet ")
                                    anotherTransaction()
                                else:
                                    print(clear)
                                    print("╔═════════════════════════════════════════════════════════╗")
                                    print("║                  Transaction Records                    ║")
                                    print("╠═════════════════════════════════════════════════════════╣")
                                    print("╠═════════════════════════════════════════════════════════╣")
                                    for record in balance[accounts.index(user)][1:]:
                                        if record % 100 == 0:
                                            print("║ You withdrawn", record, "Pesos")
                                            print("╠═════════════════════════════════════════════════════════╣")
                                        elif record % 100 != 0:
                                            record -= 1
                                            print("║ You deposited", record, "Pesos")
                                            print("╠═════════════════════════════════════════════════════════╣")
                                    anotherTransaction()

                            elif choice == "5":
                                input(complete)
                                system()
                            else:
                                print("\nInvalid input\npress enter to try again")
                                input()

                    elif password != pins[accounts.index(user)]:
                        print("Wrong PIN try again ")
                        i += 1
                    if i > 3:
                        input('\n    Too many attempts \n'
                              'press enter to login again')
                        break
                    else:
                        continue

        else:
            print("Invalid Card number")
            input('Press enter to try again')


system()
