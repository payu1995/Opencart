public class AlienCalendar {

    static String[] months = { "Ra", "Ta", "Ut", "Ip", "Ok", "Py", "Ar", "Sy", "Du", "Fi", "Gr" };
    static int[] daysInMonth = { 36, 39, 26, 29, 31, 29, 33, 34, 35, 27, 43 };
    static String[] weekDays = { "Za", "Xo", "Cu", "Vo", "Bi", "Ne", "Ma", "Lu", "Ki" };

    public static void main(String[] args) {
        PrintNMonths(2717, 9, 4);
    }

    public static void PrintNMonths(int startYear, int startMonth, int numberOfMonths) {
        for (int i = 0; i < numberOfMonths; i++) {
            printMonthHeader(startYear, startMonth - 1);
            printWeekDays();
            printMonthDays(startYear, startMonth - 1);
            
            startMonth++;
            if (startMonth > 11) {  
                startMonth = 1;
                startYear++;
            }
        }
    }

    public static void printMonthHeader(int year, int month) {
        String monthName = months[month];
        System.out.println("+------------------------------+");
        System.out.printf("| %-6s %-20d|%n", monthName, year);
        System.out.println("+------------------------------+"); 
    }

    public static void printWeekDays() {
        for (String day : weekDays) {
            System.out.printf("| %-2s ", day);
        }
        System.out.println("|");
        System.out.println("+------------------------------+");
    }

    public static void printMonthDays(int year, int month) {
        int days = adjustDaysForLeapConditions(year, month);
        int startDay = MonthStartsOn(month, year);

        int currentDayOfWeek = startDay;
        printInitialEmptySpaces(currentDayOfWeek);

        for (int day = 1; day <= days; day++) {
            System.out.printf("| %-2d ", day);
            currentDayOfWeek++;

            if (currentDayOfWeek == 9) { 
                System.out.println("|");
                currentDayOfWeek = 0;
            }
        }

        if (currentDayOfWeek != 0) {  
            for (int i = currentDayOfWeek; i < 9; i++) {
                System.out.print("|    ");
            }
            System.out.println("|");
        }
        System.out.println("+------------------------------+");
    }

    public static void printInitialEmptySpaces(int startDay) {
        for (int i = 0; i < startDay; i++) {
            System.out.print("|    ");
        }
    }

    public static int adjustDaysForLeapConditions(int year, int month) {
        int days = daysInMonth[month];
        
        if (month == 8 && isLeapYear(year)) {
            days--;
        }
        if (month == 1 && ((year * 11 + month) % 297) == 0) {  
            days++;
        }
        
        return days;
    }

    public static boolean isLeapYear(int year) {
        return year % 11 == 0; 
    }

    public static int MonthStartsOn(int monthNum, int year) {
        return (monthNum + year) % 9;
    }
}
