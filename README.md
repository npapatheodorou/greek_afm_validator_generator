# Greek AFM Validator & Generator

A modern, client-side web app for validating and generating Greek Tax Identification Numbers (AFM/TIN). It uses HTML, CSS, and JavaScript and implements the official checksum rules.

## Project Overview

This app allows users to:

- Validate a Greek AFM number
- Generate one or many AFM codes (valid or invalid)
- Customize the number of codes generated
- Use an interactive browser interface

No backend is required; everything runs in the browser.

## What Is an AFM?

AFM is Greece's Tax Identification Number (TIN), used by individuals and entities in official and financial transactions (for example, opening bank accounts, paying taxes, signing contracts, and property procedures). An AFM consists of 9 digits, where the last digit is a checksum calculated from the first 8 digits.

## Files Included

- `afm-validator-generator.html` - The main web app
- `README.md` - Documentation
- Optional assets (icons, screenshots)

## How to Use

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   ```

2. Open the HTML file in a browser:

   ```bash
   open afm-validator-generator.html
   ```

3. Use the app to validate or generate Greek AFM codes.

## AFM Checksum Explained

To determine if an AFM is structurally valid:

1. Validate that the AFM is exactly 9 numeric digits.
2. Multiply each of the first 8 digits by a power of 2:
   - Position 1 uses 2^8
   - Position 2 uses 2^7
   - ...
   - Position 8 uses 2^1
3. Sum the weighted values.
4. Compute:

   ```text
   checksum = (sum % 11) % 10
   ```

5. If the computed checksum equals the 9th digit, the AFM is structurally valid.

### Visual Diagram

```text
D1 * 2^8
D2 * 2^7
D3 * 2^6
D4 * 2^5
D5 * 2^4
D6 * 2^3
D7 * 2^2
D8 * 2^1
----------------
sum
(sum % 11) % 10
compare to D9
```

### Example Implementation (JavaScript)

```javascript
function validateAFM(afm) {
  if (!/^\d{9}$/.test(afm) || afm === "000000000") return false;

  let sum = 0;
  for (let i = 0; i < 8; i++) {
    sum += parseInt(afm[i], 10) * (1 << (8 - i));
  }
  return ((sum % 11) % 10) === parseInt(afm[8], 10);
}
```

## Notes on AFM Validity

- This app checks structural validity only; it does not verify that an AFM is officially issued or linked to a real person or entity. Official verification must be done through authorized government tools or APIs.
- The AFM is mandatory for many activities in Greece, including tax filing, banking, contracts, and property transactions.

## References

- Independent Authority for Public Revenue (AADE) - AFM assignment information
- Greek TIN (AFM) overview resources
- AFM validator/generator algorithm references and implementations

## License

This project is licensed under the MIT License.

## Contributing

Contributions are welcome:

- Open issues
- Submit pull requests
- Suggest UI/UX improvements

## Contact

For questions or help extending this project, open a GitHub issue or contact the repository owner.
