# DPMI-Consumer-Bitrate

This program is designed in Python environment. For the capturing stream, and then output will be stored in Influxdb directly and monitor in Grafana.
Installation:

1.Install automake
		sudo apt-get install automake
  Install autoconf
  		sudo apt-get install autoconf"
  Install libqd-dev
  		sudo apt-get install libqd-dev
  
 2.Then you need to install DPMI_Utils
		git clone https://github.com/DPMI/libcap_utils.git
		cd libcap_utils
		autoreconf -si
		mkdir build && cd build
		../configure
		make && make install

3. Next Install Consumer-Bitrate.
		git clone https://github.com/DPMI/consumer-bitrate.git
		cd consumer-bitrate
		make && make install
		
4.install pip:
		sudo apt-get install python-pip python-dev
		sudo pip install --upgrade pip 

5.install influxdb as shown bellow
		wget https://dl.influxdata.com/influxdb/releases/influxdb_1.3.6_amd64.deb
		sudo dpkg -i influxdb_1.3.6_amd64.deb
		sudo service influxdb start
		sudo apt-get update && sudo apt-get install influxdb
		sudo pip install influxdb

6.install Grafana as shown bellow
curl https://packagecloud.io/gpg.key | sudo apt-key add -
		sudo apt-get update
		sudo apt-get install grafana
		sudo grafana-cli plugins install mtanda-histogram-panel
		sudo service grafana-server start
	
7.install Flask as shown bellow
		sudo pip install Flask

8. Rest Api Usage:

a. After installing all the above system requirements, please change the settings(variables) before starting the "python api.py"
		change the (interface) "eth_val".
		create the database and chanege the database in "influx_db".
		change the username as required in variable "user_name". In my case user_name is stark
		change the password as required in variable "pass_word". In my case pass_word is stark
	
This tool is designed for calculating
                1. Consumer-Bitrates.
These values are plotted in Grafana by grouping technique.
RestApi manual:

Here my username:password is stark:stark

we are provided different facilities to analyse stream statistics.
1.Run stream
		curl -u username:password http:/localhost:5000/run/<stream>
2.Change stream
		curl -u username:password http:/localhost:5000/change/<stream>
3.Stop stream
		curl -u username:password http:/localhost:5000/stop
4.Show active streams
		curl -u username:password http:/localhost:5000/show
5.Add stream
		curl -u username:password http:/localhost:5000/add/<stream>
6.Delete stream
		curl -u username:password http:/localhost:5000/delete/<stream>

Next run the python api.py file in consumer-bitrate folder.
b. Grafana
1. Add the influx database to the datasource in Grafana, to display the output
2. In New dashboard option select "plugins - Histogram", use the tags "Dynamic_tag" automatically displayed with the running steams.
3. Use 'count' as aggregration and "bitrate" as measurements.
