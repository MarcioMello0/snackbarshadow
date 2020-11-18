# snackbarshadow
A shadow class for snackbars for use in Robolectric tests

Usage:
```
@RunWith(RobolectricTestRunner::class)
@Config(shadows = [ShadowSnackbar::class])
class MyTest {

    @Test
    fun snackBarCmdTest() {
        val activity = Robolectric.buildActivity(MainActivity::class.java).create().start().resume().visible().get()

        activity.doSomethingToTriggerASnackbar()

        assertThat(ShadowSnackbar.getTextOfLatestSnackbar(), 'is'(activity.getString(R.string.ok))
    }

    @Test
    fun snackBarSetTextTest() {

        val snackbar = Snackbar.make(rootView, "text of make", Snackbar.LENGTH_SHORT)
        snackbar.setText("new text")
        snackbar.show()

        assertEquals("new text", ShadowSnackbar.getTextOfLatestSnackbar())
    }
}
```