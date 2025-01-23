> 中国人です、日本語の文法が下手で申し訳ございません。コメント欄で私の間違いを指摘していただければ幸いです。

# [Tailwind CSS + IntersectionObserver] フェードイン 効果

![](/images/1.gif)

Apple の公式 Web サイトにあるようなテキストのフェードイン効果を実現するには、IntersectionObserver を使用して、テキストがウィンドウに入ったかどうかを判断します。

テキストがウィンドウに入ったら、opacity　と　translate-y　を変化する。

```tsx
export const Comp = () => {
  const ref = useRef();
  const [inView, setInView] = useState(false);

  useEffect(() => {
    if (inView) return;
    const observer = new IntersectionObserver((e) => {
      if (e?.[0].isIntersecting && !inView) {
        setInView(true);
      }
    }, {});

    if (ref.current) {
      observer.observe(ref.current);
    }
    return () => {
      observer.unobserve(ref.current);
    };
  }, [ref, inView]);


  return (
    <h1
      className={cn(
        "transition-all duration-1000",
        inView ? "opacity-100 translate-y-0" : "opacity-0 translate-y-4"
      )}
      ref={ref}
    >
      飛ぶ込み内容
    </h1>
  )
}
```
