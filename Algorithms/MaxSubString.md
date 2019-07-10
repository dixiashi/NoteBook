```
class MaxSubString
{
    static void Main(string[] args)
    {
        try
        {
            string maxSubString = string.Empty;
            string sourceString = "fasdfasoijas";

            var array = new string[]{
                null,
                string.Empty,
                "!@#$%^&*()ERTYUKBNCFM",
                "aaaaa",
                "abababababab",
                "abcabcaat",
                "abcdkkabcdk",
                "abcabcdabc",
                "abcabcdeabc",
                "abcabcdefabc",
                "abcabcdefgabc",
            };

            for (int i = 0; i < array.Length; i++)
            {
                sourceString = array[i];
                Console.WriteLine(sourceString);
                maxSubString = GetMaxSubString(sourceString);
                Console.WriteLine($"Max length is {maxSubString.Length}, Max String is {maxSubString}");
                Console.WriteLine("********************************************");
            }

        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.ToString());
        }
        finally
        {
            Console.ReadLine();
        }
    }

    /// <summary>
    /// 获取最长无重复子串
    /// 思路：
    /// 1. 保存无重复子串
    /// 2. 标记起始位置
    /// 3. 重复字符出现时，重置
    /// </summary>
    /// <data>
    ///     var array = new string[]{
    ///          null,
    ///          string.Empty,
    ///          "!@#$%^&*()ERTYUKBNCFM",
    ///          "aaaaa",
    ///          "abababababab",
    ///          "abcabcaat",
    ///          "abcdkkabcdk",
    ///          "abcabcdabc",
    ///          "abcabcdeabc",
    ///          "abcabcdefabc",
    ///          "abcabcdefgabc",
    ///      };
    /// </data>
    /// <param name="sourceString"></param>
    /// <returns>Max sub string</returns>
    private static string GetMaxSubString(string sourceString)
    {
        if (string.IsNullOrEmpty(sourceString))
        {
            return string.Empty;
        }

        int start = 0;  //最长子串起始位置
        int left = 0;   //当前子串起始位置
        int max = 0;    //最大长度

        var hash = new HashSet<char>();
        for (int i = 0; i < sourceString.Length; i++)
        {
            if (hash.Contains(sourceString[i]))
            {
                //重复字符出现时，更新最长子串起始位置
                if (hash.Count >= max)
                {
                    start = left;
                }

                //更新当前子串起始位置
                left = i;

                //重置子串
                hash.Clear();
            }

            hash.Add(sourceString[i]);
            max = Math.Max(max, hash.Count);
        }

        return sourceString.Substring(start, max);
    }

}
```
