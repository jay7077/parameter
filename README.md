import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.print("What do you want to compare? 1.area 2.perimeter:");
        int choice = input.nextInt();
        String comparisonName ="";
        if (choice == 1) {
            comparisonName = "area";
        } else if (choice == 2) {
            comparisonName = "perimeter";
        } else {
            System.out.println("Invalid choice. Program exiting.");
            return;
        }

        String shape1Name = getShapeName(input, "first");
        double shape1Dim1 = getShapeDim1(input, shape1Name);
        double shape1Dim2 = getShapeDim2(input, shape1Name);

        String shape2Name = getShapeName(input, "second");
        double shape2Dim1 = getShapeDim1(input, shape2Name);
        double shape2Dim2 = getShapeDim2(input, shape2Name);

        double shape1Size = calculateShapeSize(shape1Name, shape1Dim1, shape1Dim2, choice);
        double shape2Size = calculateShapeSize(shape2Name, shape2Dim1, shape2Dim2, choice);

        System.out.printf("%s %s: %.2f\n", shape1Name, comparisonName, shape1Size);
        System.out.printf("%s %s: %.2f\n", shape2Name, comparisonName, shape2Size);

        if (shape1Size > shape2Size) {
            System.out.printf("The %s of the %s is %.2f times bigger than the %s of the %s\n",
                    comparisonName, shape1Name, shape1Size / shape2Size, comparisonName, shape2Name);
        } else if (shape2Size > shape1Size) {
            System.out.printf("The %s of the %s is %.2f times bigger than the %s of the %s\n",
                    comparisonName, shape2Name, shape2Size / shape1Size, comparisonName, shape1Name);
        } else {
            System.out.println("The two shapes have the same size");
        }
    }

    private static String getShapeName(Scanner input, String ordinal) {
        System.out.printf("Define the %s shape: 1)rectangle 2)triangle 3)circle ", ordinal);
        int shapeChoice = input.nextInt();
        String shapeName = "";
        switch (shapeChoice) {
            case 1:
                shapeName = "rectangle";
                break;
            case 2:
                shapeName = "triangle";
                break;
            case 3:
                shapeName = "circle";
                break;
            default:
                System.out.println("Invalid shape choice. Program exiting.");
                System.exit(0);
        }
        return shapeName;
    }

    private static double getShapeDim1(Scanner input, String shapeName) {
        double dim1 = 0;
        switch (shapeName) {
            case "rectangle":
                System.out.print("Rectangle width? ");
                dim1 = input.nextDouble();
                break;
            case "triangle":
                System.out.print("Triangle base? ");
                dim1 = input.nextDouble();
                break;
            case "circle":
                System.out.print("Circle radius? ");
                dim1 = input.nextDouble();
                break;
            default:
                System.out.println("Invalid shape name. Program exiting.");
                System.exit(0);
        }
        return dim1;
    }

    private static double getShapeDim2(Scanner input, String shapeName) {
        double dim2 = 0;
        switch (shapeName) {
            case "rectangle":
                System.out.print("Rectangle height? ");
                dim2 = input.nextDouble();
                break;
            case "triangle":
                System.out.print("Triangle height? ");
                dim2 = input.nextDouble();
                break;
            case "circle":
                break;
            default:
                System.out.println("Invalid shape name. Program exiting.");
                System.exit(0);
        }
        return dim2;
    }

    private static double calculateShapeSize(String shapeName, double dim1, double dim2, int choice) {
        double size = 0;
        switch (shapeName) {
            case "rectangle":
                if (choice == 1) { // area
                    size = dim1 * dim2;
                } else if (choice == 2) { // perimeter
                    size = 2 * (dim1 + dim2);
                }
                break;
            case "triangle":
                if (choice == 1) { // area
                    size = 0.5 * dim1 * dim2;
                } else if (choice == 2) { // perimeter
                    double side3 = Math.sqrt(dim1 * dim1 + dim2 * dim2);
                    size = dim1 + dim2 + side3;
                }
                break;
            case "circle":
                if (choice == 1) { // area
                    size = Math.PI * dim1 * dim1;
                } else if (choice == 2) { // perimeter
                    size = 2 * Math.PI * dim1;
                }
                break;
            default:
                System.out.println("Invalid shape name. Program exiting.");
                System.exit(0);
        }
        return size;
    }
}
