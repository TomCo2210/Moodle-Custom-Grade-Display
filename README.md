# Custom Moodle Grade Display

This script allows you to display the grade of a specific assignment in a Moodle course on a different page. This can be useful for students who want to easily check their grades without navigating through the Moodle course.

To use this script, you will need to know the course ID and the grade ID of the assignment you want to display. You can find these values by inspecting the grade report page in Moodle.

Here's how to use the script:

1. Find the course ID and grade ID:
   - Go to the grade report page in Moodle for the course.
   - Locate the grade for the assignment you want to display.
   - Click on the grade to view the details.
   - Look at the URL of the page, which should contain the course ID and grade ID.
     - The course ID is the value of the `id` parameter in the URL.
     - The grade ID is the value of the `itemid` parameter in the URL.

2. Copy the code below:

    ```html
    <div id="grade-container" style="background-color: #f4f4f9; padding: 20px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); text-align: center;">
        <h2>{TITLE}</h2>
        <p id="grade-text">טוען את ציונך...</p>
        <p>לתשומת ליבך, הציון מורכב מממוצע ציוני כל תרגילי מקטע זה, על מנת לראות את ההערות על כל אחד מהתרגילים - יש להכנס לתרגיל עצמו.</p>
    </div>

    <iframe id="grade-iframe" src="https://moodle.afeka.ac.il/grade/report/user/index.php?id={COURSE_ID}&itemid={GRADE_ID}" style="display: none;"></iframe>

    <script>
        document.getElementById('grade-iframe').onload = function() {
            try {
                const iframeDoc = document.getElementById('grade-iframe').contentDocument || document.getElementById('grade-iframe').contentWindow.document;

                // Select the correct grade cell
                const gradeCell = iframeDoc.querySelector('td.level2.item.column-grade.cell[headers*="cat_380_"][headers*="row_"][headers*="grade"]');

                if (gradeCell) {
                    const grade = gradeCell.innerText.trim(); // Extract the grade value
                    document.getElementById('grade-text').innerHTML = `ציונך הסופי במטלה זו הוא: <strong>${grade}</strong>`;
                } else {
                    document.getElementById('grade-text').innerHTML = `לא נמצא ציון עבורך.`;
                }
            } catch (error) {
                console.error('Error loading grade:', error);
                document.getElementById('grade-text').innerHTML = `An error occurred while loading your grade.`;
            }
        };
    </script>
    ```

3. Replace the `{COURSE_ID}` and `{GRADE_ID}` attribute values in the code with the course ID and grade ID you found in step 1.

4. Customize the text in the `<h2>` and `<p>` elements to match the assignment you are displaying.

5. In the course main page, in the desired section, create a Designed Paragraph and click on the `</>` button, Paste the modified code into the code editor, and click on the `</>` button again.

6. Save the changes and view the page to see the grade displayed.

This script will load the grade for the specified assignment from the Moodle grade report page and display it on the page where you embedded the code. If the grade is found, it will be displayed in a formatted message. If the grade is not found or an error occurs, an appropriate message will be displayed.

Feel free to customize the styling and text of the displayed message to suit your needs. You can also modify the script to display grades from different assignments or courses by changing the course ID and grade ID values in the code.

