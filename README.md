# Test 
```
import UIKit
import CommonCrypto

/** 
* ทดสอบ Bytes Data Structure Base64 Encoding 
*/

extension Array where Element == UInt8 {
   
    
    func hexString(prefix: Bool) -> String {
        var str = prefix ? "0x" : ""
        
        for b in self {
            str += String(format: "%02x", b)
        }
        
        return str
    }
}

let sizeOfBytes = (32+3)*9 /// size of card + file ID + file offset + file size
let numberOfFile:UInt8 = 9
var bytes:[UInt8] = Array(repeating: 0, count: sizeOfBytes+1)

var cards:[[UInt8]] = [ [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09], [0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09,0x0A,0x00,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08,0x09]
    ]

bytes[0] = numberOfFile

var offset = 1

for i in 0..<9
{
   bytes[offset] = UInt8(i) /// File ID
   offset += 1
   bytes[offset] = 0 /// File offset
   offset += 1
   bytes[offset] = 32 /// File size
   offset += 1
   bytes[offset...offset+32-1] = cards[i][0...31]
   offset += 32
}

print("Card Datas = " + bytes.hexString(prefix: false))

let base64String = Data(bytes: bytes, count: bytes.count).base64EncodedString(options: NSData.Base64EncodingOptions(rawValue: 0))

print("Base64 = " + base64String)
```
