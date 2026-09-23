<p align="center">
<img src="cover.jpeg">
</p>

<h1 align="center">Trust but Verify: Packet Sniffing My Blink Camera's Network Traffic</h1>

<p>
I’m always fascinated with offensive security, and today I put my knowledge to the test. We have a set of Blink cameras, and for some reason, I received an email warning me about high camera data usage. This alarmed me since all my cameras are scheduled to arm at a certain time, and it was 3 hours before my scheduled arm time. I immediately contacted support, and the representative told me it was probably a glitch in their system. I ended the chat, but as someone who loves offsec, I didn't just take their word for it. I decided to investigate it myself.
</p>

<p>
I know for a fact that my home network is not perfectly secure. I currently just use a modem with a built-in router from my ISP. I don’t have the money to spend on designing enterprise-grade network infrastructure right now, but hopefully, someday I can afford it. To make sure my cameras weren't secretly recording while disarmed, I loaded up my Kali Linux VM (feeling like a hacker) and started setting up a network sniff to intercept the traffic.
</p>

<p>
I did a lot of troubleshooting before I made it to work. The first problem I faced was that my ARP spoofing tool wasn't working in my VM. My VM network was set to NAT, which isolates the VM in a virtual subnet, making it unable to send Layer 2 broadcasts to detect the camera's IP. I changed the VM to Bridged mode, but the same problem persists. I realized VMware uses MAC translation (ARP Proxy) for Wi-Fi bridging, which actively blocks forged ARP packets from leaving the host machine. Fortunately, I had USB NIC. I plugged it directly into my machine, passed it through to Kali, ran <i>ip a</i>, and voila, it pulled a proper local IP address on my physical subnet.
</p>

<p align="center">
  <b>
    Note: Do not scan networks that you don't have permission to scan! This program is intended for education purposes only. Using this program for unauthorized network scanning or malicious activities is strictly prohibited. I am not responsible for any misuse or legal repercussions that may arise from unauthorized scanning.
  </b>
</p>
