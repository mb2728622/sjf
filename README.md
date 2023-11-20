
import java.util.Scanner;
class sjf
{
    public static void main(String args[])
    {
        int burst_time[],process[],waiting_time[],tat[],i,j,n,pos,temp,total=0;
        float wait_avg,tat_avg;
        
        Scanner S = new Scanner(System.in);
        System.out.print("enter number of process:");
        n = S.nextInt();
        
        process=new int[n];
        burst_time=new int[n];
        waiting_time=new int[n];
        tat=new int[n];
        
        System.out.println("\n enter burst time:");
        for(i=0;i<n;i++)
        {
            System.out.println("\n process["+(i+1)+"]:");
            burst_time[i]=S.nextInt();
            process[i]=i+1;
        }
        
        for(i=0;i<n;i++)
        {
            pos=i;
            for(j=i+1;j<n;j++)
            {
                if(burst_time[j]<burst_time[pos])
                pos=j;
            }
            
            temp=burst_time[i];
            burst_time[i]=burst_time[pos];
            burst_time[pos]=temp;
            
            temp=process[i];
            process[i]=process[pos];
            process[pos]=temp;
        
            waiting_time[i]=0;
            for(j=0;j<i;j++)
            waiting_time[i]+=burst_time[j];
            total+=waiting_time[i];
        }
        
        wait_avg=(float)total/n;
        total=0;
        
        System.out.println("\nprocess\tburst time\twaiting time\tturnaround time");
        for(i=0;i<n;i++)
        {
            tat[i]=burst_time[i]+waiting_time[i];
            total+=tat[i];
            System.out.println("\n p"+process[i]+"\t\t"+burst_time[i]+"\t\t"+waiting_time[i]+"\t\t"+tat[i]);
        }
        
        tat_avg=(float)total/n;
        System.out.println("\n\n average waiting time :"+wait_avg);
        System.out.println("\naverage turnaround time :"+tat_avg);
        }
    }

