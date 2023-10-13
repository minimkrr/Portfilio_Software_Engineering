# Testing

## The function I chose to test 

I chose to test the part of the program where the new game in created and then the user gets a choice of easy, medium or hard. The easy mode should pick a word with less than 6 letters, the medium mode should pick a word less than 9 letters, the hard mode is any word 10 letters and above. 


```
using Hangman;
namespace HangmanTests
{
    public class UnitTest1
    {
        
            [Fact]
            public void Test_CreateNewChallengeEasy_SetWordProperty()
            {
                // Arrange
                GamePage gamePage = new GamePage("Easy");

                // Act - run method
                gamePage.CreateNewChallenge();

                // Assert - check Word is not NULL
                Assert.NotNull(gamePage.Word);
            }



    public class GamePageTests
    {
            [Theory]
            [InlineData("Easy", 6)]  // Max length for Easy is 6
            [InlineData("Medium", 9)]  // Max length for Medium is 9
            [InlineData("Hard", 100)]  // Min length for Hard is > 10
            public void Test_SelectWord_ReturnValidWordForDifferentTypes(string gameType, int expectedMaxLength)
            {
                // Arrange
                GamePage gamePage = new GamePage(gameType);

                // Act
                string selectedWord = gamePage.SelectWord(gameType);

                // Assert
                Assert.True(selectedWord.Length <= expectedMaxLength);
            }
    }
    }

}

```

## Explination and importance of tests

The first test is just checking the new challange is created correctly and is not NULL. The second test seperately runs it using each mode. It then checks for the length of the word making sure the game modes work properly picking the correct words. The tests are important to this program as without a woring difficulty option the game would not function as intended along with the first test showing us that the game initially creates and fills Word.  

## Limitations of tests

The check doesnt check if the word is actually a work of if there is a problem in the file




