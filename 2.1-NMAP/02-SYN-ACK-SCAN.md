<span style="font-size: 16px">Now lets talk about the new scan type which is SYN-ACK scan, since we already learn about the scan type TCP/IP scan this is also the same-same to the TCP/IP scan but with slightly better than that but how, if both do same thing and do same scan then how this two are different and main thing how this is better, then here comes some points why this is better,</span>

<span style="font-size: 16px">---</span>

<span style="font-size: 16px">since we almost learn how the TCP/IP scan work, it perform 3 way hands shake for establishing the connection by sending the SYN flag at first the target system response with SYN-ACK flag and then our attacker system send ACK flag then only the connection get establish and then we get knew that the ports are open or not. </span>

---

<span style="font-size: 16px">so the SYN scan also did the same thing but here comes the catch that this scan actually do slightly better job that's why it is also called </span>[***<u>half-open</u>***  ](https://www.techtarget.com/searchsecurity/definition/SYN-flooding) <span style="font-size: 16px">and the another name is </span>**<span style="font-size: 16px">Stealth Scan</span>** <span style="font-size: 16px">there is the reason to called it if we already knew about the TCP/IP scan then this also do the same thing but but but the as we know TCP/IP scan the  we know about three way hand shake on the third time when the target machine send response with with SYN-ACK flag then the SYN scan automatically send RST flag to stop the further work and stop the scan by doing only this it learn which port is open and which port is close as well as which ports are filtered. </span>

<span style="font-size: 16px">I think this much is enough for today.</span>
