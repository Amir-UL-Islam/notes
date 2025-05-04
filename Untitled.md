/* Frame 13 */

/* Auto layout */
display: flex;
flex-direction: row;
justify-content: space-between;
align-items: center;
padding: 0px;
gap: 435px;

position: absolute;
width: 1064px;
height: 44px;
left: 344px;
top: 122px;

<TextView
android:id="@+id/search_resu"
android:layout_width="125dp"
android:layout_height="24dp"
android:text="@string/search_resu"
android:textAppearance="@style/search_resu"
android:lineSpacingExtra="5sp"
android:translationY="-2.32sp"
android:gravity="top"
 />
<!--
Font family: Inter
Line height: 24sp
(identical to box height)
translationY compensates for the line height adjustment of text
-->

<!-- styles.xml -->
<style name="search_resu">
<item name="android:textSize">16sp</item>
<item name="android:textColor">#535862</item>
</style>

<!-- strings.xml -->
<string name="search_resu">
Search result for
</string>



/* Select */

width: 320px;
height: 44px;


/* Inside auto layout */
flex: none;
order: 0;
flex-grow: 0;


/* _Select input base */

/* Auto layout */
display: flex;
flex-direction: column;
align-items: flex-start;
padding: 0px;
gap: 6px;

position: absolute;
height: 44px;
left: 0px;
right: 0px;
top: 0px;



/* Input with label */

/* Auto layout */
display: flex;
flex-direction: column;
align-items: flex-start;
padding: 0px;
gap: 6px;

width: 320px;
height: 44px;


/* Inside auto layout */
flex: none;
order: 0;
align-self: stretch;
flex-grow: 0;


/* Input */

box-sizing: border-box;

/* Auto layout */
display: flex;
flex-direction: row;
align-items: center;
padding: 10px 14px;
gap: 8px;

width: 320px;
height: 44px;

/* White */
background: #FFFFFF;
/* Gray/300 */
border: 1px solid #D5D7DA;
/* Shadow/xs */
box-shadow: 0px 1px 2px rgba(10, 13, 18, 0.05);
border-radius: 8px;

/* Inside auto layout */
flex: none;
order: 0;
align-self: stretch;
flex-grow: 0;


/* Content */

/* Auto layout */
display: flex;
flex-direction: row;
align-items: center;
padding: 0px;
gap: 8px;

width: 292px;
height: 24px;


/* Inside auto layout */
flex: none;
order: 0;
flex-grow: 1;


/* search */

width: 20px;
height: 20px;


/* Inside auto layout */
flex: none;
order: 0;
flex-grow: 0;


/* Icon */

position: absolute;
left: 12.5%;
right: 12.5%;
top: 12.5%;
bottom: 12.5%;

/* Gray/500 */
border: 1.66667px solid #717680;


/* Text */

width: 53px;
height: 24px;

/* Text md/Regular */
font-family: 'Inter';
font-style: normal;
font-weight: 400;
font-size: 16px;
line-height: 24px;
/* identical to box height, or 150% */

/* Gray/500 */
color: #717680;


/* Inside auto layout */
flex: none;
order: 1;
flex-grow: 0;


/* Button */

/* Auto layout */
display: flex;
flex-direction: row;
align-items: flex-start;
padding: 0px;

width: 169px;
height: 40px;

border-radius: 8px;

/* Inside auto layout */
flex: none;
order: 1;
flex-grow: 0;


/* _Button base */

box-sizing: border-box;

/* Auto layout */
display: flex;
flex-direction: row;
justify-content: center;
align-items: center;
padding: 10px 16px;
gap: 8px;

width: 169px;
height: 40px;

/* White */
background: #FFFFFF;
/* Gray/300 */
border: 1px solid #D5D7DA;
/* Shadow/xs */
box-shadow: 0px 1px 2px rgba(10, 13, 18, 0.05);
border-radius: 8px;

/* Inside auto layout */
flex: none;
order: 0;
flex-grow: 0;


/* Text */

width: 109px;
height: 20px;

/* Text sm/Semibold */
font-family: 'Inter';
font-style: normal;
font-weight: 600;
font-size: 14px;
line-height: 20px;
/* identical to box height, or 143% */

/* Gray/700 */
color: #414651;


/* Inside auto layout */
flex: none;
order: 0;
flex-grow: 0;


/* arrow-right-01-round */

width: 20px;
height: 20px;


/* Inside auto layout */
flex: none;
order: 1;
flex-grow: 0;


/* elements */

position: absolute;
width: 5px;
height: 10px;
left: 7.5px;
top: 5px;



/* Vector */

position: absolute;
left: 37.5%;
right: 37.5%;
top: 25%;
bottom: 25%;

border: 1.5px solid #717680;
