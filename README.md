# SmartZG powered by Radiona

## LoRa
  LoRa is one of LPWAN Low Power Wide Area Network
	LoRa is IP block that describes modulation LoRa PHY
  ![IP block](http://www.bitreactive.com/wp-content/uploads/2015/09/Lora-Block.png)
	
	Lora is Proprietary modulation :(
    	Chirp spread spectrum
        	helps to get signal from noise better
          ![SNR](https://4.bp.blogspot.com/-c4caXVo-zuI/WGTx7K0etbI/AAAAAAAAGXU/nyvUa81OLIoTGopjDO3gnrHyCgsIyVktgCLcB/s1600/SF_Comparasion_7_12.png)
    	LoRa works great in a noisy environment
      ![Noisy](https://artistpictures.files.wordpress.com/2012/03/immortal-22042011-22.jpg)
      Low transmit power (25mW)
      With realy low power (40mA TX, 10mA RX)
      In sleep, chip is using under 1uA
      Low data rate
      High range
      Great battery life

	Nodes (or single chanel gateway)
		SX Chips from Semtech for different frequencies
    		EU uses 868MHz Band SX1276(433Mhz also an option with SX1278)
        		868MHz has Airtime limits
              ![AirTime](https://i2.wp.com/www.disk91.com/wp-content/uploads/2017/01/Diapositive12.png?w=720&ssl=1)

        
    	Gateway SX1301/SX1308 for gateway 
        	Can receive 8 bands at the same time
        	Has better sensitivity
    
    	Chips are SPI controlled
    
    	868 is a license-free band :)
    	125kHz bandwidth
        	https://www.disk91.com/2017/technology/internet-of-things-technology/all-what-you-need-to-know-about-regulation-on-rf-868mhz-for-lpwan/
        	https://i2.wp.com/www.disk91.com/wp-content/uploads/2017/01/Diapositive12.png?w=720&ssl=1
        	https://i2.wp.com/www.disk91.com/wp-content/uploads/2017/01/ResauxLowPower.png?w=720&ssl=1

    	Check gr-LoRa on git
        	https://github.com/BastilleResearch/gr-lora

## LoRaWAN
        LoRaWAN is a media access control (MAC) protocol for wide area networks. It is designed to allow low-powered devices to
        communicate with Internet-connected applications over the long range wireless connections.
            https://stackforce.github.io/LoRaMac-doc/group___l_o_r_a_m_a_c.html

        It is Encrypted (AES-128)

	    Half-Duplex communication - transmission of data in just one direction at a time (walkie-talkie) 

    	ISM bands 915 US 868 in EU
        	In EU you can send only 1% of the time on some frequencies 0.1%
        	One band 10% of the time
    	
        1% of time is just 36 seconds in one hour

        Time spendt on air depends of SF and message lenght
            Great picture of AIR time

        Protocol is supporting 3 classes
    	Class A
        	Sends Opens RX1 Opens RX2 Got to sleep
    	Class B 
        	Sends and receives in adjusted time slots
    	Class C 
        	Sends Opens RX1 waits with opened RX2

        Gateway has same airtime limits as the node - you can use 10% band for downlink

        Sends back message on same frequency, message has arrived RX1, or on special frequency RX2
    
        Two way for node to attach to a network
        Two keys, one for network server and one for data (application)
        OTAA
            Handshaking
            Device sends request
            Gateway calculates the session key
            Node calculates session keys
                Note that no key is sent by node nor by gw
            Gateway sends accept (settings) encrypted with new keys
                https://image.slidesharecdn.com/apricot17-lpwagivingavoicetothings-rel4-61488325419-170306004415/95/lpwa-giving-a-voice-to-things-48-638.jpg?cb=1488761088

        ABP Authorisation by personalisation
            You just set the session key on both sides (keys never change so it is less secure)
        
        LoRa is not for a lot of data, and not for time-critical data

        Listen Before Talk (feature of some new gateways)
            The Listen Before Talk (LBT) protocol makes it possible for multiple users to share the same channel. 
            When LBT is enabled, the device continuously monitors channels so as to transmit only when a channel is not in use.

        Newest MAC supports repeaters

        Gateway is just Forwarder  just forwarding messages from NODE <> Network
            Packet forwarder - runs on node

        Network architecture
            https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fimage.slidesharecdn.com%2Florawansynchronizationsemtech-151117212231-lva1-app6891%2F95%2Florawan-iot-synchronization-7-638.jpg%3Fcb%3D1447795408&f=1

        Complete opensource solution
            Gateway bridge
                Packet FW <> GW bridge
            Network server broker
            Application server broker

        or use TTN - https://www.thethingsnetwork.org/
            v3 should be easier to deploy on your servers

        Remember LoRa is all about compromise
            https://ubidots.com/blog/wp-content/uploads/2017/07/pick-2-.jpg


TTNZagreb by radiona (SmartZG)
Two workshops for now
    Build your GW
    All about nodes - mapping the city

Coverage of our gateways
    TTN mapper
        Not opensource
    check lemilica.com for open source solution

Use case
    IRNAS has few great ones
        Count penguins
            power on
            take pic
            OpenCV count penguins
            lora send no of penguins
            power off
        Pit stop for turtles
        Trap for poachers
    Birdhouse
        Bird in - temp
    Intrudes alarm on some distant place - or boat...
    Public scale
        On exibition - visit us @
    Pager
    GPS for pets
    Polution detector
        If something bad detected send a warning
    Agriculture
    Distant plant soil moisture

    So many other

Warning:
    Do not put your GW near a working chimney
