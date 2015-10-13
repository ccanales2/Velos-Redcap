# Velos-Redcap
Trying to integrate Velos with RedCap

With this project, I am trying to create a connection between both systems. Velos is an incredible clinical trials management system (CTMS) but has room for improvement with the electronic case report forms (eCRFs). REDCap is a great tool to create eCRFS and reporting has a direct SPPS output. This is a powerful tool for research teams that don't necessarily have a biostatistician.

The connection that I am currently working on is this:

1. Export from Velos. Eventually I will access the tables in Velos, specifically the demographic information sans patient identifiers
2. ETL - Use SSIS to map the outputs from Velos to a local .csv file
3. 3. Using Python, I will use the API from REDCap to upload the file directly. This way, the fields and data are simply uploaded thus creating fields and data in REDCap.
4. This would allow nice direct output to SPSS. Also, reporting for institutions would be easier. The systems would mirror each other therefore eliminating inconsistencies in "numbers.


<h2>Setup, thus far</h2>

I'm using PyCap (@sburns) to tap into REDCap. Here is that part of it

$ pip install requests
$ git clone git://github.com/sburns/PyCap.git PyCap
$ cd PyCap
$ python setup.py install

Now my specifics...(with the help of @sburns

import redcap
from redcap import Project, RedcapError
url = 'https://########YOUR REDCAP URL#####/api'
token = '##### YOUR REDCAP API  #####'
project = Project(url, token)

import csv
with open('C:\\####location of csv file####') as fobj:
...:  reader = csv.DictReader(fobj)
...:  data = [row for row in reader]

count = project.import_reader(data)


