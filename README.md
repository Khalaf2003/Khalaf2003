
#include <iostream>
#include <map>
#include <sstream>

using namespace std;

map<char, string> charToMorse = {
    {'A', ".-"}, {'B', "-..."}, {'C', "-.-."}, {'D', "-.."}, {'E', "."}, {'F', "..-."},
    {'G', "--."}, {'H', "...."}, {'I', ".."}, {'J', ".---"}, {'K', "-.-"}, {'L', ".-.."},
    {'M', "--"}, {'N', "-."}, {'O', "---"}, {'P', ".--."}, {'Q', "--.-"}, {'R', ".-."},
    {'S', "..."}, {'T', "-"}, {'U', "..-"}, {'V', "...-"}, {'W', ".--"}, {'X', "-..-"},
    {'Y', "-.--"}, {'Z', "--.."},
    {'1', ".----"}, {'2', "..---"}, {'3', "...--"}, {'4', "....-"}, {'5', "....."},
    {'6', "-...."}, {'7', "--..."}, {'8', "---.."}, {'9', "----."}, {'0', "-----"}
};

string textToMorse(const string& text) {
    stringstream result;
    for (char c : text) {
        if (c == ' ') {
            result << "   "; // 3 spaces for word separation
        } else {
            result << charToMorse[toupper(c)] << " "; // Use map to get Morse code for each character
        }
    }
    return result.str();
}

string morseToText(const string& morse) {
    stringstream result;
    stringstream ss(morse);
    string code;
    while (ss >> code) {
        for (const auto& entry : charToMorse) {
            if (entry.second == code) {
                result << entry.first;
                break;
            }
        }
    }
    return result.str();
}

int main() {
    string plainText = "I love C plus plus";
    string morseText = textToMorse(plainText);
    cout << "Plain text: " << plainText << endl;
    cout << "Morse text: " << morseText << endl;

    string originalText = morseToText(morseText);
    cout << "Original text: " << originalText << endl;

    return 0;
}

