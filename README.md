import java.util.Arrays;
import java.util.Scanner;
import java.util.Objects;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number of students");
        int number = sc.nextInt();
        sc.nextLine();
        String[][] list = new String[number][2];
        String[] goodman = new String[number];
        int sum = 0;
        int b = 0;

        
        for (int i = 0; i < number; i++) {
            System.out.println("Enter the name of the " + (i + 1) + "th student");
            list[i][0] = sc.nextLine();
            System.out.println("Enter the corresponding score");
            int gd = sc.nextInt();
            sc.nextLine();
            if (gd > 90) {
                goodman[b] = list[i][0];
                b++;
            }
            list[i][1] = String.valueOf(gd);
            sum += gd;
        }

        System.out.println("The grade point average is: " + (double) sum / number);
        String[] goodmanTrimmed = new String[b];
        System.arraycopy(goodman, 0, goodmanTrimmed, 0, b);
        System.out.println(Arrays.deepToString(list));
        if (goodmanTrimmed.length == 0) {
            System.out.println("No one is above ninety");
        } else {
            System.out.println("There are more than 90 people: " + Arrays.toString(goodmanTrimmed));
        }
        for (String[] strings : list) {
            for (String s : strings) {
                System.out.print(s + " ");
            }
            System.out.println();
        }

    
        while (true) {
            System.out.println("What function do you want to implement?");
            System.out.println("A: Add a new student");
            System.out.println("B: Find a student's score");
            System.out.println("C: Delete a student");
            System.out.println("D: Exit");
            String choice = sc.nextLine();
            String[][] newList = null;

            if (Objects.equals(choice, "A") || Objects.equals(choice, "a")) {
                System.out.println("Enter the name of the new student");
                String newName = sc.nextLine();
                System.out.println("Enter the grade of the new student");
                int newGrade = sc.nextInt();
                sc.nextLine();
                newList = new String[list.length + 1][2];
                for (int i = 0; i < list.length; i++) {
                    newList[i] = list[i].clone();
                }
                newList[list.length][0] = newName;
                newList[list.length][1] = String.valueOf(newGrade);
            } else if (Objects.equals(choice, "B") || Objects.equals(choice, "b")) {
                System.out.println("Enter the name of the student you want to find");
                String theName = sc.nextLine();
                boolean found = false;
                for (String[] strings : list) {
                    if (theName.equals(strings[0]) && strings.length > 0) {
                        System.out.println(theName + "'s score is " + strings[1]);
                        found = true;
                        break;
                    }
                }
                if (!found) {
                    System.out.println("Student not found");
                }
            } else if (Objects.equals(choice, "C") || Objects.equals(choice, "c")) {
                System.out.println("Enter the name of the student you want to delete");
                String nameToDelete = sc.nextLine();
                boolean deleted = false;

               
                newList = new String[list.length - 1][2];
                int newIndex = 0;

              
                for (int i = 0; i < list.length; i++) {
                    if (!nameToDelete.equals(list[i][0])) {
                        newList[newIndex] = list[i];
                        newIndex++;
                    } else {
                        deleted = true;
                    }
                }

                if (deleted) {
                    list = newList;
                    System.out.println(Arrays.deepToString(list)); 
                    System.out.println("Student " + nameToDelete + " has been deleted successfully.");
                } else {
                    System.out.println("Student not found. Unable to delete.");
                }
            } else if (Objects.equals(choice, "D") || Objects.equals(choice, "d")) {
                break;
            } else {
                System.out.println("Invalid choice. Please choose A, B, C, or D.");
            }

            if (newList!= null) {
                list = newList;
            }
        }
    }
}
