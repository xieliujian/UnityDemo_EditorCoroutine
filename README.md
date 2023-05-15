# 编辑器协程

## 示例

```cs

[MenuItem("EditorCoroutine/Test")]
static void Test()
{
    EditorCoroutine.StartEditorCoroutine(CountToTenCoroutine());
}

private static IEnumerator CountToTenCoroutine()
{
    for (var i = 1; i <= 10; ++i)
    {
        Debug.LogFormat("{0}", i);

        // yield until next EditorApplication.update
        yield return null;

        // yield until 1 second has passed
        yield return new WaitForSeconds(1);
    }

    // yield until a subroutine has completed
    yield return CountToTenCompletedSubroutine();
}

private static IEnumerator CountToTenCompletedSubroutine()
{
    Debug.LogFormat("DONE!");

    yield break;
}

```