

def error(expression):
    not_start_with = "+-/*="
    if expression == "/exit":
        return "Bye!"
    elif expression == "/help":
        return "The program calculates the sum, subtraction, division, multiplication and power of numbers!"
    elif expression[0].startswith("/"):
        return "Unknown command"
    elif expression[-1] in not_start_with:
        return "Invalid expression"
    elif "(" in expression and ")" not in expression:
        return "Invalid expression"


def priority(priority_expression):
    open_index = -1
    close_index = -1
    for i in priority_expression:
        if "(" in i:
            open_index = priority_expression.index(i)
        elif ")" in i and priority_expression.index(i) > open_index:
            close_index = priority_expression.index(i)
            break

    return open_index, close_index


def signals(signal):
    if len(signal) == 1:
        return signal
    elif signal == "++" or signal == "--":
        return "+"
    elif signal == "+-" or signal == "-+":
        return "-"
    elif signal == "+++":
        return "+"
    elif signal == "---":
        return "-"
    elif signal == "*":
        return "*"
    elif signal == "/":
        return "/"
    elif signal == "**":
        return "**"
    else:
        # new_signal = signals(signal[:3]) + signals(signal[3:])
        # return signals(new_signal)
        return "Invalid expression"


def calc_priority_parenthisis(open, close, initial_expression):
    priority_expression = []

    if open >= 0 and close >= 0:
        priority_expression = initial_expression[open:close + 1]
    elif open >= 0 and close == -1:
        return "Invalid expression"
    elif open == -1 and close >= 0:
        return "Invalid expression"

    for i in priority_expression:
        if "(" in i:
            a = priority_expression.index(i)
            priority_expression[a] = i.replace("(", "")

        elif ")" in i:
            a = priority_expression.index(i)
            priority_expression[a] = i.replace(")", "")

    control_expression = []
    for i in priority_expression:
        if "" != i:
            control_expression.append(i)

    priority_expression = calc_rest(control_expression)
    return priority_expression


def calc_rest(expression_to_calc):
    for i in range(1, len(expression_to_calc), 2):
        if expression_to_calc[i][0] in operators:
            expression_to_calc[i] = signals(expression_to_calc[i])

    for i in expression_to_calc:
        for k, v in dictionary.items():
            if i == k:
                expression_to_calc = list(map(lambda x: x.replace(i, v), expression_to_calc))

    while True:
        if "**" in expression_to_calc:
            i = expression_to_calc.index("**")
            calculation = int(expression_to_calc[i - 1]) ** int(expression_to_calc[i + 1])
            if i == 1:
                expression_to_calc = [calculation] + expression_to_calc[i + 2:]
            else:
                expression_to_calc = expression_to_calc[: i - 1] + [calculation] + expression_to_calc[i + 2:]

        elif "*" in expression_to_calc:
            i = expression_to_calc.index("*")
            calculation = int(expression_to_calc[i - 1]) * int(expression_to_calc[i + 1])
            if i == 1:
                expression_to_calc = [calculation] + expression_to_calc[i + 2:]
            else:
                expression_to_calc = expression_to_calc[: i - 1] + [calculation] + expression_to_calc[i + 2:]

        elif "/" in expression_to_calc:
            i = expression_to_calc.index("/")
            calculation = int(expression_to_calc[i - 1]) // int(expression_to_calc[i + 1])
            if i == 1:
                expression_to_calc = [calculation] + expression_to_calc[i + 2:]
            else:
                expression_to_calc = expression_to_calc[ : i - 1] + [calculation] + expression_to_calc[i + 2:]

        elif "+" in expression_to_calc:
            i = expression_to_calc.index("+")
            calculation = int(expression_to_calc[i - 1]) + int(expression_to_calc[i + 1])
            if i == 1:
                expression_to_calc = [calculation] + expression_to_calc[i + 2:]
            else:
                expression_to_calc = expression_to_calc[: i - 1] + [calculation] + expression_to_calc[i + 2:]

        elif "-" in expression_to_calc:
            i = expression_to_calc.index("-")
            calculation = int(expression_to_calc[i - 1]) - int(expression_to_calc[i + 1])
            if i == 1:
                expression_to_calc = [calculation] + expression_to_calc[i + 2:]
            else:
                expression_to_calc = expression_to_calc[: i - 1] + [calculation] + expression_to_calc[i + 2:]

        else:
            break

        if len(expression_to_calc) == 1:
                break

    if len(expression_to_calc) == 1:
        return expression_to_calc[0]
    else:
        return "Invalid expression"


dictionary = {}
alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
operators = "+-*/"


while True:
    user_express = input()

    if user_express == "":
        continue

    elif error(user_express):
        if error(user_express) == "Bye!":
            print(error(user_express))
            break
        elif error(user_express) != "":
            print(error(user_express))
            continue

    else:
        user_express = user_express.replace("=", " = ")
        user_express = user_express.replace("+", " + ")
        user_express = user_express.replace("-", " - ")
        user_express = user_express.replace("*", " * ")
        user_express = user_express.replace("/", " / ")

        user_express_split = user_express.split()

        i = 0
        while i < len(user_express_split):
            if user_express_split[i] in operators and user_express_split[i + 1] in operators:
                user_express_split = user_express_split[:i] + [
                    "".join(user_express_split[i:i + 2])] + user_express_split[i + 2:]
                i -= 1

            elif user_express_split[i][0] in operators and user_express_split[i + 1] in operators:
                user_express_split = user_express_split[:i] + [
                    "".join(user_express_split[i:i + 2])] + user_express_split[i + 2:]
                i -= 1
            i += 1

        while True:
            if "(" in user_express or ")" in user_express:
                while True:
                    for i in user_express_split:
                        if "((" in i:
                            a = user_express_split.index(i)
                            user_express_split[a] = i.replace("((", "(")
                            user_express_split.insert(a, "(")
                        elif "))" in i:
                            a = user_express_split.index(i)
                            user_express_split = user_express_split[a].replace("))", ")")
                            user_express_split = user_express_split.insert(")", a)

                    open_par, close_par = priority(user_express_split)

                    result = calc_priority_parenthisis(open_par, close_par, user_express_split)

                    user_express_split = user_express_split[: open_par] + [str(result)] + user_express_split[close_par + 1:]

                    user_express = " ".join(user_express_split)

                    if "Invalid expression" in user_express_split:
                        user_express_split = "Invalid expression"
                        break
                    elif len(user_express_split) == 1:
                        result = user_express_split
                        break
                    elif "(" not in user_express and ")" not in user_express:
                        break
                    else:
                        continue

                if len(user_express_split) == 1:
                    break
                else:
                    continue


            if user_express in dictionary.keys():
                print(dictionary[user_express])
                break

            elif "=" in user_express_split[1]:
                key = user_express_split[0]
                value = user_express_split[2]
                dictionary[key] = value
                break

            else:
                result = calc_rest(user_express_split)
                print(result)
                break
