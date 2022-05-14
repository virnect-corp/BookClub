# EXERCISE 2.6

This exercise helps you recognize what concepts you are familiar with and what concepts are harder for you by testing your code reading memory. The underlying assumption is that, as shown by the experiments outlined, familiar concepts are easier to remember. What you can remember is what you know, so these exercises can be used for (self) diagnosis of your code knowledge.

## Step 1: Select code

Select a codebase you are somewhat familiar with—maybe something you work with regularly, but not mainly. It can also be something you personally wrote a while ago. Make sure you have at least some knowledge of the programming language the code is written in. You have to know more or less what the code does, but not know it intimately. You want to be in a situation similar to the chess players; they know the board and the pieces but not the setup.

In the codebase, select a method or function, or another coherent piece of code roughly the size of half a page, with a maximum of 50 lines of code.

**Answer**

you work with regularly, but not mainly. 이런 코드가 뭐가 있나 생각하다가 작년에 만든 listview에 대한 코드 일부를 가져와 보면 재미있겠다는 생각이 들었다.

그 코드는 유창님이 작업한 코드이지만 실제 설계 부분과 코드 리뷰를 내가 진행했기에 짧은 코드 부분을 가져와서 첨부해 본다.

## Step 2: Study code

Study the selected code for a bit, for a maximum of two minutes. Set a timer so you don’t lose track of the time. After the timer runs out, close or cover the code.

**Answer**

우선 ctrl+c, ctrl+v를 빠르게 하고 타이머를 돌려 2분간 탐색하고 끝내자마자 바로 visual code로 작성해 봤다.

종이에 쓰면 사진을 찍어야 하고 IDE로 하기엔 또 다른 툴을 열어야 하는 번거로움이 있어서 바로 md 파일에 작성을 시작했다.

``` c#
public class ListView : PullScrollView, IListView, IEditMode
{
    private ObservableCollection<IItem> dataList = new ObservableCollection<IItem>();
    public GameObject ItemPrefab;
    public UnityEvent<IListView> OnInitializeAdd;
    public UnityEvent<IItem> OnItemClick;
    public UnityEvent<IItem, bool> OnItemSelect;

    protected override void Awake()
    {
        dataList.CollectionChanged += new NotifyCollectionChangedEventHandler(ListDataChanged);
        OnBottomPull.AddListener(Initialize);
        OnTopPull.AddListener(RefreshData);
    }

    protected override void OnDestroy()
    {
        dataList.CollectionChanged -= new NotifyCollectionChangedEventHandler(ListDataChanged);
        OnBottomPull.RemoveListener(Initialize);
        OnTopPull.RemoveListener(RefreshData);
    }

    void ListDataChanged(object sender, NotifyCollectionChangedEventArgs e)
    {
        if (e.Action == NotifyCollectionChangedAction.Reset)
        {
            content.GetComponentsInChildren<ListItemViewModel>().ToList().ForEach(item => Destroy(item.gameObject));
        }
        else if (e.Action == NotifyCollectionChangedAction.Remove)
        {
            // e.OldItems count is 1
            foreach (IItem item in e.OldItems)
            {
                ListItemViewModel listItemViewModel = content.GetComponentsInChildren<ListItemViewModel>().ToList().Find(listItemViewModel => listItemViewModel.item.Equals(item));
                if (listItemViewModel != null)
                {
                    Destroy(listItemViewModel.gameObject);
                }
            }
        }
        else if (e.Action == NotifyCollectionChangedAction.Add)
        {
            // e.NewItems count is 1
            foreach (IItem item in e.NewItems)
            {
                GameObject gameObject = Instantiate(ItemPrefab, content);
                ListItemViewModel viewModel = gameObject.GetComponent<ListItemViewModel>();
                viewModel.SetData(item);
                viewModel.clickEvent = OnItemClick;
                viewModel.OnItemChecked += OnItemCheckedEvent;
                viewModel.IsEditMode = isEditMode;
            }
        }
    }

    private void OnItemCheckedEvent(IItem item, bool isCheck) => OnItemSelect?.Invoke(item, isCheck);

    public void RefreshData()
    {
        dataList.Clear();
        ScrollToTop();
        Initialize();
    }

    private void Initialize() => OnInitializeAdd?.Invoke(this);

    // ...
}
```

## Step 3: Reproduce the code

Take a piece of paper, or open a new file in your IDE, and try to recreate the code as best as you can.

**Answer**

``` c#
public class ListView
{
    public ObservableCollection<ItemData> listData = new ObservableCollection<ItemData>();
    protected void Awake()
    {
        listData.OnItemChanged += OnItemChanged(object sender, NotifyObjectItemChanged e);
    }

    protected void OnDestroy()
    {
        listData.OnItemChanged -= OnItemChanged(object sender, NotifyObjectItemChanged e);
    }

    private void OnItemChanged(object sender, NotifyObjectItemChanged e)
    {
        if (e.ItemChanged == Item.Add)
        {

        }
        else if (e.ItemChanged == Item.Reset)
        {

        }
        else if (e.ItemChanged == Item.Remove)
    }
}
```

## Step 4: Reflect

When you are sure you have reproduced all the code you possibly can, open the original code and compare. Reflect using these questions:

- Which parts did you produce correctly with ease?
- Are there any parts of the code that you reproduced partly?
- Are there parts of the code that you missed entirely?
- Do you understand why you missed the lines that you did?
- Do the lines of code that you missed contain programming concepts that are unfamiliar to you?
- Do the lines of code that you missed contain domain concepts that are unfamiliar to you?

**Answer**

Which parts did you produce correctly with ease?

- ObservableCollection. 이 클래스 객체가 핵심적인 역할을 수행하고 있기 때문

Are there any parts of the code that you reproduced partly?

- 거의 없음. 기억을 할 수 있었던 건 메서드 이름 정도인데 이 마저도 LTM에 의존한 기억임.

Are there parts of the code that you missed entirely?

- 거의 전체를 다 보지 못한 것 같다. 필드 일부, 메서드 5개가 있다는 것 정도만 기억했다.

Do you understand why you missed the lines that you did?

- 짧은 시간에 많은 걸 기억하기에는 한계가 있다는게 느껴졌다. 평소에 코드를 기억해 내는 훈련을 안하고 있다가 테스트 해보니 안되고 있다는 느낌이 많이 든다.

Do the lines of code that you missed contain programming concepts that are unfamiliar to you?

- 익숙하지 않은 개념은 없었는데, 클래스 이름이 상당히 길어서 이걸 기억해내기가 어려웠다. NotifyCollectionChangedEventArgs의 경우 기억하기를 포기했다.

Do the lines of code that you missed contain domain concepts that are unfamiliar to you?

- 도메인 지식은 거의 없었다. 어떤 리스트에 변화가 감지되면 추가, 삭제 하는 코드라서 그 안에 item에 해당하는 데이터가 어떤 도메인을 나타내는지 나오는 코드는 아니었다.

## Step 5: Compare with someone else (optional)

If you have a coworker who wants to improve their chunking abilities too, you can do this exercise together. It can be very interesting to reflect on the differences in the code you reproduce. Because we know there are large differences between beginners and experts, this exercise might also help you understand your level of skill in a programming language relative to someone else’s.

**Answer**

서로 재현한 코드를 비교해 보고 기억력 테스트가 아닌 어떤 chunking 능력을 발휘해서 작성했는지 비교해 보고 스스로 어떤 수준의 프로그래밍 능력을 가졌는지 확인해 보는 시간을 가지면 좋겠습니다.
