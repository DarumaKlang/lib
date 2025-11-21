# Update

## V.1.1

ผมได้ปรับปรุงโค้ดส่วน **Mode 1** ในไฟล์ `src/components/TriplexGridFinder.tsx` ให้แสดงชื่อตัวแปร (เช่น "ฤทธี / อัตตะ") ต่อท้ายพิกัดทันทีครับ

คุณสามารถ **Copy โค้ดเฉพาะส่วนนี้** ไปทับส่วนเดิมในไฟล์ `TriplexGridFinder.tsx` ได้เลยครับ:

### 💻 โค้ดที่ปรับปรุง (เฉพาะส่วน render ของ Mode 1)

ค้นหาบรรทัดที่เป็น `{columnMajorPosition ? (` แล้วแทนที่ด้วยโค้ดชุดนี้ครับ:

```tsx
           <div className="w-full sm:w-1/2 text-center">
                {columnMajorPosition ? (
                    <div className="animate-fadeIn">
                        <p className="text-gray-500 text-sm mb-1">ตำแหน่งของคุณคือ</p>
                        
                        {/* 1. แสดงพิกัด R | C */}
                        <div className="text-3xl font-extrabold text-blue-600">
                        R{columnMajorPosition.row} <span className="text-gray-300 mx-1">|</span> C{columnMajorPosition.column}
                        </div>

                        {/* 2. [เพิ่มใหม่] แสดงชื่อตัวแปรที่เชื่อมโยง */}
                        <div className="mt-3 p-2 bg-white border border-blue-100 rounded-md shadow-sm">
                        <p className="text-lg text-gray-800 font-bold">
                            {getVariableName(columnMajorPosition.row, columnMajorPosition.column)}
                        </p>
                        </div>

                        <p className="text-xs text-gray-400 mt-2">Slot Index: {columnMajorPosition.slotIndex}</p>
                    </div>
                ) : (
                    <p className="text-red-400 text-sm italic">กรุณาใส่เลข 1-99</p>
                )}
            </div>
```

-----

### สิ่งที่เพิ่มเข้ามา :

ผมได้เพิ่มกล่องแสดงข้อความด้านล่างพิกัด R|C โดยเรียกใช้ฟังก์ชัน `getVariableName` ครับ

```tsx
<div className="mt-3 p-2 bg-white border border-blue-100 rounded-md shadow-sm">
    <p className="text-lg text-gray-800 font-bold">
        {getVariableName(columnMajorPosition.row, columnMajorPosition.column)}
    </p>
</div>
```

ตอนนี้เมื่อคุณพิมพ์เลขลำดับ เช่น **50** ระบบจะแสดงผลว่า:

  * **R2 | C3**
  * **โพงน้ำป่า / สหัชชะ** (ชื่อตัวแปรที่ดึงมาจาก Data)
  * Slot Index: 8

ลองอัปเดตแล้วรันดูได้เลยครับ\!
