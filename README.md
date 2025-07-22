Project: Suspicious Network Traffic Analysis and Data Exfiltration Recovery
Objective
To conduct a full investigation based on a captured network traffic file (challenge.pcapng), identify potential data exfiltration via unauthenticated file sharing, reconstruct the transmitted data, and extract any hidden content. This project demonstrates hands-on skills in:

Network packet analysis (PCAP)

File carving and binary data recovery

Hash cracking

Archive extraction

Hidden data extraction (QR decoding)

Tools and Technologies Used
Category	Tools
Network analysis	Wireshark
Archive handling	unzip, zipinfo
Hash cracking	CrackStation (MD5 hash cracker)
Image/QR analysis	Google Lens, Online QR Scanner
Operating System	Kali Linux / Ubuntu (TryHackMe VM)

Step-by-Step Breakdown
1. Inspecting challenge.pcapng in Wireshark
Opened the .pcapng file using Wireshark.

tcp.stream eq 0
Followed the TCP stream → changed view to Raw → saved the output as file.zip.

2. Detecting Credentials or Secrets
Inside the TCP stream, an MD5 hash was identified:

90eb7723a657b6597100aafef171d9f2
Assumed to be the password for the transmitted ZIP archive.

3. Cracking the MD5 Hash
Submitted the hash to CrackStation.
Password: avengers

5. Extracting the ZIP Archive
Unzipped the archive using:

unzip file.zip
Entered password avengers, successfully extracted the file secrets.png.

5. Analyzing the Extracted Image
The file secrets.png turned out to be a QR code.

Scanned the QR code using Google Lens / an online QR reader.

Recovered the final flag:

THM{n0t_s3cur3_f1l3_sh4r1ng}

Outcome
Recovered Flag:
THM{n0t_s3cur3_f1l3_sh4r1ng}
The investigation confirms that an unencrypted ZIP archive containing sensitive data was transferred over the network, with its password exposed as a raw MD5 hash in the traffic — highlighting poor security practices and lack of encryption in file sharing services.

Key Takeaways
Effective use of Wireshark to filter and inspect TCP streams.

Manual reconstruction of transmitted binary files.

Cracking unsalted MD5 hashes with public databases.

Secure handling of encrypted ZIP archives.

QR code analysis for hidden/encoded content extraction.

A complete and structured approach to forensic analysis.

