import java.math.BigInteger;
import java.util.*;
import org.json.JSONObject;

public class PolynomialSolver {

    public static BigInteger convertToDecimal(String value, int base) {
        return new BigInteger(value, base);
    }

    // Lagrange interpolation to find f(0) (constant term)
    public static BigInteger lagrangeAtZero(int[] x, BigInteger[] y, int k) {

        BigInteger result = BigInteger.ZERO;

        for (int i = 0; i < k; i++) {

            BigInteger term = y[i];

            for (int j = 0; j < k; j++) {
                if (i != j) {
                    BigInteger numerator = BigInteger.valueOf(-x[j]);
                    BigInteger denominator = BigInteger.valueOf(x[i] - x[j]);
                    term = term.multiply(numerator).divide(denominator);
                }
            }

            result = result.add(term);
        }

        return result;
    }

    public static void main(String[] args) {

        String jsonInput = "{ YOUR_JSON_HERE }";

        JSONObject obj = new JSONObject(jsonInput);

        JSONObject keys = obj.getJSONObject("keys");
        int k = keys.getInt("k");

        int[] x = new int[k];
        BigInteger[] y = new BigInteger[k];

        int index = 0;

        for (String key : obj.keySet()) {

            if (key.equals("keys")) continue;

            if (index >= k) break;

            JSONObject root = obj.getJSONObject(key);

            int base = Integer.parseInt(root.getString("base"));
            String value = root.getString("value");

            x[index] = Integer.parseInt(key);
            y[index] = convertToDecimal(value, base);

            index++;
        }

        BigInteger secret = lagrangeAtZero(x, y, k);

        System.out.println("Constant term (secret): " + secret);
    }
}
