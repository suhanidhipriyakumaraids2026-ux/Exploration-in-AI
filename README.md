# Exploration-in-AI
class Solution {
private:
    long long getSmallestPrimeFactor(long long n) {
        if (n % 2 == 0) return 2;
        for (long long i = 3; i * i <= n; i += 2) {
            if (n % i == 0) return i;
        }
        return n;
    }

public:
    long long minimumMaxValue(int n, int index, int value) {
        // Step 1: Validate left side (from index down to 0)
        long long curr = value;
        for (int i = index - 1; i >= 0; --i) {
            long long prev = -1;
            if (curr % 2 == 0) {
                prev = curr - 2;
            } else {
                long long spf = getSmallestPrimeFactor(curr);
                prev = curr - spf;
            }

            if (prev <= 0) return -1;
            curr = prev;
        }

        // Step 2: Build right side (from index up to n - 1)
        curr = value;
        for (int i = index + 1; i < n; ++i) {
            if (curr % 2 == 0) {
                curr += 2;
            } else {
                curr += getSmallestPrimeFactor(curr);
            }
        }

        return curr;
    }
};
