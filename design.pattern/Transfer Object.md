# Transfer Object 패턴
* Value Object라고도 불리는 Transfer Object는 데이터를 전송하기 위한 객체에 대한 패턴입니다.
* Transfer Object 패턴은 Transfer Object를 만들어 하나의 객체에 여러 타입의 값을 전달하는 일을 수행합니다.

```
public class PstReact {

  private int commentId;
  private int userId;
  private int postId;

  public PstReact() {
    super();
  }

  public PstReact(int commentId, int userId, int postId) {
    super();
    this.commentId = commentId;
    this.userId = userId;
    this.postId = postId;
  }

  public int getUserId() {
    return userId;
  }

  public void setUserId(int userId) {
    this.userId = userId;
  }

  public int getPostId() {
    return postId;
  }

  public void setPostId(int postId) {
    this.postId = postId;
  }

  public int getCommentId() {
    return commentId;
  }

  public void setCommentId(int commentId) {
    this.commentId = commentId;
  }

  @Override
  public String toString() {
    StringBuilder sb = new StringBuilder();
    return sb.toString();
  }
}
```

Transfer Object를 사용할 때 필드를 private로 지정해서 getter(), setter() 메소드를 만들어야 할 지
아니면 그냥 필드를 public으로 지정할 지에 대해 정답은 없지만,
성능상으로 따져볼 때 getter()와 setter()를 만들지 않는 것이 더 빠릅니다.
하지만, 정보를 은닉하고, 모든 필드의 값들을 아무나 마음대로 수정할 수 없게 하려면
getter(), setter() 메소드를 작성하는 것이 일반적이다.
또, Transfer Object를 생성할 때는 반드시 toString() 메소드를 구현하는 것을 권장합니다.

* 이 패턴을 사용한다고 엄청난 성능 개선 효과가 있는 것은 아니다. 하지만, 하나의 객체에 결과 값을 담아올 수 있어
두 번, 세 번씩 요청하는 일이 발생하는 것을 줄여주기 때문에, 이 패턴을 사용하기를 권장합니다.