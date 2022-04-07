# Erasure Codes

Erasure codes are how we protect against data erasure due to disk failure or some other catastrophic erasure event. The idea is to protect a database, which might be large and spread across multiple hard drives, but without needing to back up the entire database. The way we do this is with erasure codes, which is a type of error correction.

Modern digital information technology is superior to analog technology because we can introduce error correction schemes and repeaters to repeat messages without amplifying noise. In an analog system, to retransmit a message, we have to relay the original message/information, which means we will amplify any noise that accompanies it. There are only so many retransmissions possible, before the original message or information is completely drowned out by noise.

In a digital system however, we use _repeaters_ to pass on information. A repeator has a memory (buffer), and the message or information contains some sort of error correction scheme that the repeator applies to the message to correct for errors due to noise, then retransmit the corrected message or information. The birth of this strategy is generally attributed to Richard Hamming, who pioneered the first Forward Error Correction schemes, and the Hamming Distance for self-correcting error codes.

In terms of erasure codes, information stored across multiple hard drives is like information at a repeater. The system stores the information on a big buffer (the many disks) and there is a possibility that some of the information gets corrupted or deleted on one of the disks. But, because we apply an erasure coding scheme to the data, if one disk dies, we can use the error correction to reconstitute all the information on the dead disk. This takes up some extra overhead or disk space, but not nearly as much as having to backup the entire database.

In technical terms, an erasure coding scheme takes the data and breaks it into _fragments_. To go with these fragments, the coding scheme generates _parity fragments_. All these fragments are spread across disks. If one disk dies, we can use the parity fragments on the other live disks to reconstitute the lost data.

That's a rough overview of erasure codes.
