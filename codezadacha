def get_ring_substring(s, start, length):
    n = len(s)
    start %= n
    if length == 0:
        return ""
    if start + length <= n:
        return s[start:start+length]
    else:
        part1 = s[start:]
        remaining = length - (n - start)
        part2 = s[:remaining]
        return part1 + part2

def main():
    with open("input.txt", "r") as f:
        s = f.read().strip()
    
    n = len(s)
    if n < 3:
        with open("output.txt", "w") as out:
            out.write("No")
        return
    
    digits = [int(char) for char in s]
    
    def get_number(start, length):
        num = 0
        start %= n
        if start < 0:
            start += n
        if start + length <= n:
            for i in range(start, start + length):
                num = num * 10 + digits[i]
        else:
            for i in range(start, n):
                num = num * 10 + digits[i]
            rem = length - (n - start)
            for i in range(0, rem):
                num = num * 10 + digits[i]
        return num

    for start in range(n):
        for a_len in range(1, n - 1):
            if a_len > 1 and digits[start] == 0:
                continue
                
            candidates = set()
            cand1 = n - 2 * a_len
            if 1 <= cand1 <= n - a_len - 1 and a_len >= cand1:
                candidates.add(cand1)
                
            cand2 = n - 2 * a_len - 1
            if 1 <= cand2 <= n - a_len - 1 and a_len >= cand2:
                candidates.add(cand2)
                
            total = n - a_len
            if total % 2 == 0:
                cand3 = total // 2
                if 1 <= cand3 <= n - a_len - 1 and cand3 >= a_len:
                    candidates.add(cand3)
                    
            cand4_val = total - 1
            if cand4_val >= 0:
                cand4 = cand4_val // 2
                if 2 * cand4 == cand4_val:
                    if 1 <= cand4 <= n - a_len - 1 and cand4 >= a_len:
                        candidates.add(cand4)
            
            for b_len in candidates:
                c_len = n - a_len - b_len
                if c_len < 1:
                    continue
                    
                startB = (start + a_len) % n
                if b_len > 1 and digits[startB] == 0:
                    continue
                    
                startC = (start + a_len + b_len) % n
                if c_len > 1 and digits[startC] == 0:
                    continue
                    
                A = get_number(start, a_len)
                B = get_number(startB, b_len)
                C = get_number(startC, c_len)
                
                if A + B == C:
                    A_str = get_ring_substring(s, start, a_len)
                    B_str = get_ring_substring(s, startB, b_len)
                    C_str = get_ring_substring(s, startC, c_len)
                    with open("output.txt", "w") as out:
                        out.write(f"{A_str}+{B_str}={C_str}")
                    return
                        
    with open("output.txt", "w") as out:
        out.write("No")

if __name__ == "__main__":
    main()
