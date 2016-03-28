struct Node{
    int data;
    Node* next;
};

//O(1)时间删除链表节点，从无头单链表中删除节点
void deleteRandomNode(Node *cur)
{
    assert(cur != NULL);
    assert(cur->next != NULL);    //不能是尾节点
    Node* pNext = cur->next;
    cur->data = pNext->data;
    cur->next = pNext->next;
    delete pNext;
}


//单链表的转置,循环方法
Node* reverseByLoop(Node *head)
{
    if(head == NULL || head->next == NULL)
        return head;
    Node *pre = NULL;
    Node *next = NULL;
    while(head != NULL)
    {
        next = head->next;

        head->next = pre;
        pre = head;
        head = next;
    }
    return pre;
}

//单链表的转置,递归方法
Node* reverseByRecursion(Node *head)
{
    //第一个条件是判断异常，第二个条件是结束判断
    if(head == NULL || head->next == NULL) 
        return head;

    Node *newHead = reverseByRecursion(head->next);

    head->next->next = head;
    head->next = NULL;

    return newHead;    //返回新链表的头指针
}

//倒数第k个节点
Node* theKthNode(Node *head,int k)
{
    if(k < 0) return NULL;    //异常判断

    Node *slow,*fast;
    slow = fast = head;
    int i = k;
    for(;i>0 && fast!=NULL;i--)
    {
        fast = fast->next;
    }

    if(i > 0)    return NULL;    //考虑k大于链表长度的case

    while(fast != NULL)
    {
        slow = slow->next;
        fast = fast->next;
    }

    return slow;
}
