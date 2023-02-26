// Create a function called isAnagram, which given two strings, returns true if they are anagrams of one another.
// For example: `Listen` is an anagram of `Silent`

function isAnagram(first, second) {
  //code goes here
}

 isAnagram(s1, s2) {
      const st1 = s1.toLowerCase().replace(/[^\w]/g, '');
      const st2 = s2.toLowerCase().replace(/[^\w]/g, '');

      const new_st1 = st1.split('').sort().join('');
      const new_st2 = st2.split('').sort().join('');

      return new_st1 === new_st2;
  }
