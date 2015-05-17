# Repository-9
Modify class Time2 of Fig. 8.5 to include a tick method that increments the time stored in a Time2 object by one second. Provide method incrementMinute to increment the minute by one and method incrementHour to increment the hour by one. The Time2 object should always remain in a consistent state. Write a program that tests the tick method, the incrementMinute method and the incrementHour method to ensure that they work correctly. Be sure to test the following cases: a) incrementing into the next minute, b) incrementing into the next hour and c) incrementing into the next day (i.e., 11:59:59 PM to 12:00:00 AM).


public class Time3
{
   private int hour;
   private int minute; 
   private int second; 

   public Time3()
   {
      this(0, 0, 0);
   } 

   public Time3(int hour) 
   { 
      this(hour, 0, 0);
   } 

   public Time3(int hour, int minute) 
   { 
      this(hour, minute, 0);
   } 
   
   public Time3(int hour, int minute, int second) 
   { 
      if (hour < 0 || hour >= 24)
         throw new IllegalArgumentException("hour must be 0-23");

      if (minute < 0 || minute >= 60)
         throw new IllegalArgumentException("minute must be 0-59");

      if (second < 0 || second >= 60)
         throw new IllegalArgumentException("second must be 0-59");
      

      this.hour = hour;
      this.minute = minute; 
      this.second = second; 
	   /*if (hour >= 0 || hour < 24)
		   this.hour = hour;
	   if (minute >= 0 || minute < 60)
		   this.minute = minute; 
	   if (second >= 0 || second < 60)
		   this.second = second;*/
   } 
   
   public Time3(Time3 tick)
   {
      this(tick.getHour(), tick.getMinute(), tick.getSecond());
   } 


   // Set Methods
   // set a new time value using universal time; 
   // validate the data
   public void setTime(int hour, int minute, int second)
   {
      if (hour < 0 || hour >= 24)
         throw new IllegalArgumentException("hour must be 0-23");
    	 
      if (minute < 0 || minute >= 60)
         throw new IllegalArgumentException("minute must be 0-59");
    
      if (second < 0 || second >= 60)
         throw new IllegalArgumentException("second must be 0-59");
     
      this.hour = hour;
      this.minute = minute; 
      this.second = second;
	   /*if (hour >= 0 || hour < 24)
		   this.hour = hour;
	   if (minute >= 0 || minute < 60)
		   this.minute = minute; 
	   if (second >= 0 || second < 60)
		   this.second = second;*/
   } 

   // validate and set hour 
   public void setHour(int hour) 
   { 
	   //if (hour >= 0 || hour < 24)
      if (hour < 0 || hour >= 24)
         throw new IllegalArgumentException("hour must be 0-23");

      this.hour = hour;
   } 

   // validate and set minute 
   public void setMinute(int minute) 
   { 
	   //if (minute >= 0 || minute <60)
	   
      if (minute < 0 || minute >= 60)
    	  throw new IllegalArgumentException("minute must be 0-59");

      this.minute = minute; 
   } 

   // validate and set second 
   public void setSecond(int second) 
   { 
	   //if (second >= 0 || second <60)
      if (second < 0 || second >= 60)
         throw new IllegalArgumentException("second must be 0-59");

       this.second = second; 
   } 

   // Get Methods
   // get hour value
   public int getHour() 
   { 
      return hour; 
   } 

   // get minute value
   public int getMinute() 
   { 
      return minute; 
   } 

   // get second value
   public int getSecond() 
   { 
      return second; 
   } 
   
   public void incrementSecond()
   {
      //setSecond(second+1);
      
      if(second<59)
      {
    	  setSecond(second+1);
          //incrementMinute();
      }
      else
      {
    	  setSecond(0);
    	  incrementMinute();
      }
    	  
   }
   
   //increment minute method
   public void incrementMinute()
   {
      //setMinute(minute+1);
      
      if(minute<59)
      {
         setMinute(minute+1);
         //incrementHour();
      }
      else
      {
    	  setMinute(0);
    	  incrementHour();
      }
     /* if(minute==0)
      {
    	  incrementHour();
      }*/
   }
   
   //increment hour method
   public void incrementHour()
   {
	   //setHour(hour+1);
	   
	   if(hour<23)
	   {
		   setHour(hour+1);
	   }
	   else
		{
		   setHour(0); 
		}
   }
   
	   

   // convert to String in universal-time format (HH:MM:SS)
   public String toUniversalString()
   {
      return String.format(
         "%02d:%02d:%02d", getHour(), getMinute(), getSecond());
   } 

   // convert to String in standard-time format (H:MM:SS AM or PM)
   public String toString()
   {
      return String.format("%d:%02d:%02d %s", 
         ((getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12),
         getMinute(), getSecond(), (getHour() < 12 ? "AM" : "PM"));
   } 
}
//Test Program

// Fig. 8.6: Time2Test.java
// Overloaded constructors used to initialize Time2 objects.

import java.util.Scanner;

public class Time3Test
{// Start class

   public static void main( String[] args )
   {// Start main method
   
      Scanner input=new Scanner(System.in);
      
      //object created to show tick
      Time3 tick=new Time3();
      
      //requesting time from user
      System.out.println("Please enter the time below");
      System.out.printf("Please enter Hours: ");
      int hour=input.nextInt();
      tick.setHour(hour);
      
      System.out.printf("Please enter Minutes: ");
      int minute=input.nextInt();
      tick.setMinute(minute); 
      
      System.out.printf("Please enter Second: ");
      int second=input.nextInt();
      tick.setSecond(second);
      
      //displaying time entered from user in Universal and 12 hours format
      System.out.println("\nTime in Universal format: "+tick.toUniversalString());
      System.out.println("Time in 12 hours format:  "+tick.toString());
      
      //displaying time after adding one second in 12 hours and Universal format
      tick.incrementSecond();
      System.out.println("\nUniversal time after adding one second: "+tick.toUniversalString());
      System.out.printf("Time after adding one second: %s",tick.toString());

      //displaying time after adding one minute in 12 hours and Universal format
      tick.incrementMinute();
      System.out.println("\n\nUniversal time after adding one minute: "+tick.toUniversalString());
      System.out.printf("Time after adding one minute: %s",tick.toString());

      //displaying time after adding one hour in 12 hours and Universal format
      tick.incrementHour();
      System.out.println("\n\nUniversal time after change: "+tick.toUniversalString());
      System.out.printf("Time after adding one hour: %s",tick.toString());
   
   }
}
