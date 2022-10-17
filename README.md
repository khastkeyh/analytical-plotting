#This code is used in reading txt file and plotting the required data
# -*- coding: utf-8 -*-
"""
Created on Wed Oct 12 20:41:14 2022
@author: YusufZiyaDemirbas
"""
import numpy as np
import matplotlib.pyplot as plt

def extract_data(inname1):
    infile1 = open(inname1,"r")
    drop = []
    temp = []
    time = []
    infile1.readline()
    
    for line in infile1:
        line.strip()
        
        a = line.find("\t")
        b = line.rfind("\t")
        t = line[a:b]
        t = float(t)
        temp.append(t)
        
        x = line[b:]
        x = float(x)
        time.append(x)
      
        dr = line[:a]
        dr = float(dr)
        drop.append(dr)
    infile1.close()
    return(drop,temp,time)

def plotData(inputfile):
    drop,temp,time = extract_data(inputfile)
    
    plt.clf()
    #temperature dependent drop plot
    plt.subplot(1,2,1)
    plt.plot(drop,temp,"b:.",linestyle='-', marker='o', markersize=2, alpha=0.4, color="black")
    plt.xlabel("Drop")
    plt.ylabel("Temperature")
    plt.title("Temperature dependent drop plot")
    plt.grid("on")
    plt.grid("off")
    plt.subplots_adjust(top=0.9)
    plt.tight_layout(h_pad=0.9)

    #Time dependent drop plot
    plt.subplot(1,2,2)
    plt.plot(time,drop,"r:.",)
    plt.xlabel("Time(minute)")
    plt.ylabel("Drop")
    plt.title("Time dependent drop plot")
    plt.grid("on")
    plt.grid("off")
    plt.subplots_adjust(top=0.9)
    plt.tight_layout(h_pad=0.9)

#Example I used 
plotData("datas_ethanol-water.txt")
plotData("datas_cyclohexane-toluene")
