# Save-sensor-in-a-data-file
C# script made for saving data files
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System.IO;

public class DataCollector : MonoBehaviour
{
    
    string filename = "";
    [System.Serializable]


    public class Data
    {
        public float x;
        public float y;
        public float z;
    }
    [System.Serializable]
    public class DataGathered
    {
        public Data[] sensor;
    }

    public DataGathered newDataGathered = new DataGathered();
    public bool Activated = false;

    // Start is called before the first frame update
    void Start()
    {
        filename = Application.dataPath + "/Data.csv";
        TextWriter tw = new StreamWriter(filename, false);
        tw.WriteLine("x,y,z");
        tw.Close();
    }

    // Update is called once per frame
    void Update()
    {
        if (Activated == true)
        {
            WriteToCSV();
        }

    }

    public void OnTrigger()
    {
        if (Activated == true)
        {
            Activated = false;
        }
        else if (Activated == false)
        {
            Activated = true;

        }
    }

    public void WriteToCSV()
    {
        if (newDataGathered.sensor.Length > 0)
        {
            TextWriter tw = new StreamWriter(filename, true);
            tw.Close();

            tw = new StreamWriter(filename, true);



            for (int i = 0; i < newDataGathered.sensor.Length; i++)
            {

                newDataGathered.sensor[i].x = Input.acceleration.x;
                newDataGathered.sensor[i].y = Input.acceleration.y;
                newDataGathered.sensor[i].z = Input.acceleration.z;
                tw.WriteLine(newDataGathered.sensor[i].x + "," + newDataGathered.sensor[i].y + "," + newDataGathered.sensor[i].z);


            }
            tw.Close();

       
        }

    }
}
