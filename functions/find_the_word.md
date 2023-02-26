/*
Let us define a precedence string as follows:
"F>E" means that in the word, the letter "F" comes before the letter "E".

The objective of this test is to implement the find_the_word function.
When passed a list of precedences, the function will return the word associated to the input.
There are no duplicate letters in the word.

For example:
------------

findTheWord(["G>W","W>F"]) should return GWF
findTheWord(["E>R","R>S","S>O","O>N","P>E"]) should return PERSON

*/

function findTheWord(letters) {
   let output = [];
        let [a, b] = '';
        let indexA = '';
        let indexB = '';

        for (let i = 0; i < letters.length; i++) {
          [a, b] = letters[i].split(">");
          indexA = output.indexOf(a);
          indexB = output.indexOf(b);
          if (indexA === -1 && indexB === -1) {
            output.push(a, b);
          } else if (indexA === -1) {
            output.splice(indexB, 0, a);
          } else if (indexB === -1) {
            output.splice(indexA + 1, 0, b);
          } else if (indexA < indexB) {
            continue;
          } else {
            return null;
          }
        }
        return output.join("");
}
