# Temp

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;  
import java.io.IOException;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;


public class createJSON {  

    public static void main(String[] args) throws FileNotFoundException, IOException {  


        String country="";
        String population="";
        String gdp ="";
        String line="";

        String fileName = "C:\\Parts\\country.csv";
        String jsonfile="C:\\Parts\\Json_batch.json";
        Scanner scanner = new Scanner(new File(fileName));
        File jfile=new File(jsonfile);
        jfile.delete();
        jfile.createNewFile();

        FileWriter fileWriter = new FileWriter(jfile,true);
        fileWriter.write("{ \"countries\":[");
        //Set the delimiter used in file
        while( scanner.hasNextLine())
        {
            line=scanner.nextLine();
            Scanner linesc=new Scanner(line);
            linesc.useDelimiter(",");

           while (linesc.hasNext())
            {
                country=linesc.next();
                population=linesc.next();
                gdp = linesc.next();

                System.out.println("Country | Population | GDP = "+country+"|"+population+"|"+gdp);
                country=country.replaceAll("\\n", "");
                population=population.replaceAll("\\n", "");
                gdp=gdp.replaceAll("\\n", "");

                JSONObject countryObj = new JSONObject();
                countryObj.put("Country", country);
                countryObj.put("GDP", gdp);
                countryObj.put("Population", population);




                System.out.println("Print ready:" +countryObj.toJSONString());
                fileWriter.write(countryObj.toJSONString());

                if(scanner.hasNext()) {
                    fileWriter.write(",");
                }
            }
        }

        fileWriter.write("]}");
        fileWriter.close();
        //Do not forget to close the scanner

        scanner.close();

    }
}
