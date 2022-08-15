# Java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

       
        Quiz quiz = new Quiz();
        quiz.begin();

    }
}

class Quiz
{
    void begin()
    {
        Question[] questions = new Question[5];

        questions[0] = new Question("DATA STRUCTURE \nWhich of the following is not the type of queue?\n","Priority Queue","Single-ended Queue","Circular Queue","Ordinary Queue", new Answer("Single-ended Queue"));
        
        
        questions[1] = new Question("What function is used to append a character at the back of a string in C++?","push_back()","append()","push","insert()", new Answer("push_back()"));
        
        
        questions[2] = new Question("Which one of the following is an application of queue data structure","When a resource is shared among multiple users","When data is transferred asynchronously","Load balancing","All of the", new Answer("All of the above"));
        
        
        questions[3] = new Question("Which of the following data structures allow insertion and deletion from both ends?","Stack","Deque","Queue","Strings", new Answer("Deque"));
        
        
        questions[4] = new Question("Which of the following sorting algorithms provide the best time complexity in the worst-case scenario?","Merge Sort","Quick Sort","Bubble Sort","Selection Sort", new Answer("Merge Sort"));
        
        
     

        int countTotal = 0;
        int countRight = 0;
        int countWrong = 0;

        for(Question q: questions) 
        {
            System.out.println(q.getQuestion());
            System.out.println("A : " +q.getOption1());
            System.out.println("B : " +q.getOption2());
            System.out.println("C : " +q.getOption3());
            System.out.println("D : " +q.getOption4());

            String answer = "";

            char ans;
            System.out.println("Enter your answer");
            Scanner scan = new Scanner(System.in);
            ans = scan.next().charAt(0);

            switch(ans)
            {
                case 'A':
                case 'a':
                    answer = q.getOption1();
                    break;
                case 'B':
                    case 'b':
                    answer = q.getOption2();
                    break;
                case 'C':
                    case 'c':
                    answer = q.getOption3();
                    break;
                case 'D':
                    case 'd':
                    answer = q.getOption4();
                    break;
                default:break;
            }
            System.out.println("Your answer " + answer + " " + q.getAnswer().getAnswer());
            if(answer.equals(q.getAnswer().getAnswer()))
            {
                System.out.println("------------------------------------------------------");
                System.out.println("                  Correct Answer                      ");
                System.out.println("------------------------------------------------------");
                countRight++;
            }
            else
            {
                System.out.println("------------------------------------------------------");
                System.out.println("                  Wrong Answer                      ");
                System.out.println("------------------------------------------------------");
                countWrong++;
            }
            System.out.println("============================================================================================");
            countTotal++;
        }

        Result result = new Result(countTotal,countRight,countWrong);
        result.showResult();
    }
}

class Question
{

    String question;
    String option1;
    String option2;
    String option3;
    String option4;
    Answer answer;

    public Question(String question, String option1, String option2, String option3, String option4, Answer answer) {
        this.question = question;
        this.option1 = option1;
        this.option2 = option2;
        this.option3 = option3;
        this.option4 = option4;
        this.answer = answer;
    }

    public String getQuestion() {
        return question;
    }

    public String getOption1() {
        return option1;
    }

    public String getOption2() {
        return option2;
    }

    public String getOption3() {
        return option3;
    }

    public String getOption4() {
        return option4;
    }

    public Answer getAnswer() {
        return answer;
    }
}

class Answer
{
    String answer;

    public Answer(String answer) {
        this.answer = answer;
    }

    public String getAnswer() {
        return answer;
    }
}

interface IResult
{
    void showResult();
    double showPercentage(int correctAnswers,int totalQuestions);
    String showPerformance(double percentage);
}

class Result implements IResult
{
    int totalQuestions;
    int correctAnswers;
    int wrongAnswers;

    public Result(int totalQuestions, int correctAnswers, int wrongAnswers) {
        this.totalQuestions = totalQuestions;
        this.correctAnswers = correctAnswers;
        this.wrongAnswers = wrongAnswers;
    }

    @Override
    public void showResult() {
        System.out.println("Your results!");
        System.out.println("Total Questions " + totalQuestions);
        System.out.println("Number of correct answers " + correctAnswers);
        System.out.println("Number of wrong answers " + wrongAnswers);
        System.out.println("Percentage " + showPercentage(correctAnswers,totalQuestions));
        System.out.println("Your performance " + showPerformance(showPercentage(correctAnswers,totalQuestions)));

    }

    @Override
    public double showPercentage(int correctAnswers, int totalQuestions) {
        //System.out.println(correctAnswers + " " + totalQuestions);
        return (double) (correctAnswers / (double)totalQuestions) * 100 ;
    }

    @Override
    public String showPerformance(double percentage) {
        String performance = "";

        if(percentage > 70)
        {
            performance = "Good";
        }
        else if(percentage < 30)
        {
            performance = "Poor";
        }

        return performance;

    }
}
