package machine

fun main() {

    val processing = Processing(400, 540, 120, 9, 550)

    do {
        val option = processing.inputOption(readln())
    } while (option)
}

// main class
class Processing(
    var waterInMachine: Int,
    var milkInMachine: Int,
    var beansInMachine: Int,
    var cupsInMachine: Int,
    var moneyInMachine: Int
) {
    var status = CurrentStatus.MENU

    init {
        textInMenu(status)
    }

    // function for navigation in menu
    fun inputOption(input: String): Boolean {
        status = when (status) {
            CurrentStatus.MENU -> actions(input)
            CurrentStatus.BUY -> buying(input)
            CurrentStatus.FILL_WATER -> filling_water(input)
            CurrentStatus.FILL_MILK -> filling_milk(input)
            CurrentStatus.FILL_BEANS -> filling_beans(input)
            CurrentStatus.FILL_CUPS -> filling_cups(input)
            else -> CurrentStatus.MENU
        }
        textInMenu(status)
        return status != CurrentStatus.EXIT
    }

    // function for output text in menu
    fun textInMenu(status: CurrentStatus) = when (status) {
        CurrentStatus.MENU -> println("Write action (buy, fill, take, remaining, exit): ")
        CurrentStatus.REMAINING -> println(
            "The coffee machine has:\n" +
                    "$waterInMachine ml of water\n" +
                    "$milkInMachine ml of milk\n" +
                    "$beansInMachine g of coffee beans\n" +
                    "$cupsInMachine disposable cups\n" +
                    "$$moneyInMachine of money"
        )
        CurrentStatus.BUY -> println("What do you want to buy? 1 - espresso, 2 - latte, 3 - cappuccino, back - to main menu: ")
        CurrentStatus.FILL_WATER -> println("Write how many ml of water do you want to add: ")
        CurrentStatus.FILL_BEANS -> println("Write how many grams of coffee beans do you want to add: ")
        CurrentStatus.FILL_MILK -> println("Write how many ml of milk do you want to add: ")
        CurrentStatus.FILL_CUPS -> println("Write how many disposable cups of coffee do you want to add: ")
        CurrentStatus.TAKE -> println("I gave you $$moneyInMachine")
        CurrentStatus.ERROR -> println("Error. Please enter valid input")
        CurrentStatus.EXIT -> println("")
    }

    // function for actions in main menu
    fun actions(input: String): CurrentStatus {
        return when (input) {
            "buy" -> {
                CurrentStatus.BUY
            }
            "fill" -> {
                CurrentStatus.FILL_WATER
            }
            "take" -> {
                textInMenu(CurrentStatus.TAKE)
                moneyInMachine = 0
                CurrentStatus.MENU
            }
            "remaining" -> {
                textInMenu(CurrentStatus.REMAINING)
                CurrentStatus.MENU
            }
            "exit" -> {
                CurrentStatus.EXIT
            }
            else -> {
                textInMenu(CurrentStatus.ERROR)
                CurrentStatus.MENU
            }
        }

    }

    // function for buying beverage
    fun buying(input: String): CurrentStatus {
        return when (input) {
            "1" -> making_coffee(Coffee.Espresso)
            "2" -> making_coffee(Coffee.Latte)
            "3" -> making_coffee(Coffee.Cappuccino)
            "back" -> CurrentStatus.MENU
            else -> CurrentStatus.BUY
        }
    }

    // function for refilling of water
    fun filling_water(input: String): CurrentStatus {
        val addedWater = input.toInt()
        waterInMachine += addedWater
        return CurrentStatus.FILL_MILK
    }

    // function for refilling of milk
    fun filling_milk(input: String): CurrentStatus {
        val addedMilk = input.toInt()
        milkInMachine += addedMilk
        return CurrentStatus.FILL_BEANS
    }

    // function for refilling of coffee beans
    fun filling_beans(input: String): CurrentStatus {
        val addedCoffee = input.toInt()
        beansInMachine += addedCoffee
        return CurrentStatus.FILL_CUPS
    }

    // function for refilling of disposable cups
    fun filling_cups(input: String): CurrentStatus {
        val addedCups = input.toInt()
        cupsInMachine += addedCups
        println()
        return CurrentStatus.MENU
    }

    // function for preparing coffee
    fun making_coffee(coffee: Coffee): CurrentStatus {
        if (check_ingredients(coffee)) {
            println("I have enough resources, making you a coffee!\n")
            plus_minus(coffee)
        }
        return CurrentStatus.MENU
    }

    // function for changing ingredients after making a coffee
    fun plus_minus(coffee: Coffee) {
        waterInMachine -= coffee.waterForCoffee
        milkInMachine -= coffee.milkForCoffee
        beansInMachine -= coffee.beansForCoffee
        cupsInMachine--
        moneyInMachine += coffee.priceOfCoffee
    }

    // function for "not enough" ingredients
    fun check_ingredients(coffee: Coffee): Boolean {
        val notEnoughIngredients = mutableListOf<String>()
        when {
            waterInMachine < coffee.waterForCoffee -> notEnoughIngredients.add("water")
            milkInMachine < coffee.milkForCoffee -> notEnoughIngredients.add("milk")
            beansInMachine < coffee.beansForCoffee -> notEnoughIngredients.add("coffee beans")
            cupsInMachine <= 0 -> notEnoughIngredients.add("cups")
        }
        if (notEnoughIngredients.size > 0) {
            println("Sorry, not enough ${notEnoughIngredients.joinToString(",")}!")
        }
        return notEnoughIngredients.size == 0
    }
}

// coffees values' enum
enum class Coffee(
    val waterForCoffee: Int,
    val milkForCoffee: Int,
    val beansForCoffee: Int,
    val priceOfCoffee: Int
    ) {
    Espresso(250, 0, 16, 4),
    Latte(350, 75, 20, 7),
    Cappuccino(200, 100, 12, 6)
    }

// class to determine current stage
enum class CurrentStatus {
    MENU,
    BUY,
    REMAINING,
    TAKE,
    FILL_WATER,
    FILL_MILK,
    FILL_BEANS,
    FILL_CUPS,
    ERROR,
    EXIT
}
