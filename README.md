# HackTheBox.eu Deadly Arthropod Write-Up

This was a really fun exercise and a lesson to be taught, that USB keyboard keystrokes can be captured as a pcap file.

Originally, I was stumped, and looked online to find this <a href="https://medium.com/@ali.bawazeeer/kaizen-ctf-2018-reverse-engineer-usb-keystrok-from-pcap-file-2412351679f4">original keymapper</a>

The original keystroke mapper was pretty shoddy and did not consider CAPITALIZED characters. A better solution I found here <a href="https://bitvijays.github.io/LFC-Forensics.html">better keymapper</a>

# Solution

First use tshark to strip out only the keyscans

<code>tshark -r deadly_arthropod.pcap -T fields -e usb.capdata > keystrokes.txt</code>

When you program the script and run it the first time, make sure you clear out empty whitespaces from the capture file with the <code>cat keystrokes.txt | awk 'NF' > pipe;cat pipe > keystrokes.txt</code> command. Otherwise the script will throw an error as it does not interpret empty lines.

Originally I received two faux keys and one final string of gibberish that I did not understand.

<code>eks@hackthebox.eu</code>
<code>Th1sC0uldB3MyR3alP@ssw0rd</code>
<code>QK<_>.<<<<H>5<<{_<I>>ck>'>>b0<<<<<<<<<I<<<<T>>f>>>>>>_>>>>>>}<.<.<<<<3<<<<<<<<u<<t_>>a<<<<<<<<<<B>>>>>>>>>>>>>>t>5<<<I>>>_>>>>>a<<<<<<a>>>>>>d<<<<y>>>r
</code>

You're not done yet. On line 3, follow the keystrokes, '<' is left arrow, and '>' is right arrow. If you did it correctly, you will find the key as:

<code>
HTB{If_It_Quack5_It'5_a_K3yb0ard...}
</code>

Submit it and get your points!

![](https://raw.githubusercontent.com/tanc7/HacktheBox_Deadly_Arthropod_Writeup/master/challengesolved.png)

# Conclusion

This was a very fun exercise and I enjoyed it, particularly how pcap file formats can be used to capture keystrokes as well.

There were at least two public sources of Hacking/Cybersecurity CTF match write-ups to cite from. If you use my second script <code>translate_attempt_2.py</code> you will get the same result and properly register CAPITALIZED letters that were missing in the first script. Registering the [shift] key is critical to solving the challenge. Be patient with the left and right arrows, following them closely will reveal the typed out flag.

