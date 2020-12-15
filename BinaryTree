#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#define NR 11	/*根的指针数*/
#define MAXSIZE 20 /*存储数据元素的最大个数*/
#define TRUE 1
#define FALSE 0
#define ERROR NULL
#define STRLEN 200

typedef struct TreeNode *BinTree;
typedef struct TreeNode{
	char Data;
	BinTree Left;
	BinTree Right;
    BinTree Parent; /*建立哈夫曼树时使用*/
}TreeNode;

BinTree root[NR];
int Cur_Num;

typedef TreeNode HTreeNode;
typedef BinTree HTree;
typedef struct IndexNode{
    char Data;
    char Code[MAXSIZE]; /*Path*/
    struct IndexNode *Next;
}IndexNode, *IndexLink;

typedef struct QNode{
	BinTree Data[MAXSIZE];
	int Rear;	/*队列尾元素位置*/
	int Front;	/*队列头元素位置*/
}QNode, *Queue;

typedef struct SNode{
	BinTree Data[MAXSIZE];
	int Top;/*栈顶位置*/
}SNode, *Stack;

Queue CreateQueue(void)
{
	Queue Q=(Queue)malloc(sizeof(QNode));
	Q->Front=Q->Rear=0;
	return Q;
}

int IsFullQ(Queue Q)
{
	return((Q->Rear+1)%MAXSIZE==Q->Front);
}

_Bool AddQ(Queue PtrQ,BinTree item)
{
	if(IsFullQ(PtrQ))
	{
		printf("队列满\n");
		return FALSE;
	}
	PtrQ->Rear=(PtrQ->Rear+1)%MAXSIZE;
	PtrQ->Data[PtrQ->Rear]=item;
	return TRUE;
}

int IsEmptyQ(Queue Q)
{
	return(Q->Front==Q->Rear);
}

BinTree DeleteQ(Queue PtrQ)
{
	if(IsEmptyQ(PtrQ))
	{
		printf("队列空\n");
		return NULL;
	}
	else
	{
		PtrQ->Front=(PtrQ->Front+1)%MAXSIZE;
		return PtrQ->Data[PtrQ->Front];
	}
}/* Queue */

Stack CreateStack(void)
{
	Stack S=(Stack)malloc(sizeof(SNode));
	S->Top=-1;
	return S;
}

int IsFullS(Stack PtrS)
{
	return(PtrS->Top==MAXSIZE-1);
}

_Bool Push(Stack PtrS,BinTree item)
{
	if(IsFullS(PtrS))
	{
		printf("堆栈满\n");
		return FALSE;
	}
	else
	{
		PtrS->Data[++(PtrS->Top)]=item;
		return TRUE;
	}
}

int IsEmptyS(Stack PtrS)
{
	return(PtrS->Top==-1);
}

BinTree Pop(Stack PtrS)
{
	if(IsEmptyS(PtrS))
	{
		printf("堆栈空\n");
		return NULL;
	}
	else
	{
		return(PtrS->Data[(PtrS->Top)--]);
	}
}/* Stack */

_Bool InitBinTree(BinTree *PtrBT)
{
    *PtrBT=NULL;
    return TRUE;
}/* Num:1 */

void DestroyBinTree(BinTree *PtrBT)
{
	if(*PtrBT)
	{
		DestroyBinTree(&((*PtrBT)->Left));
		DestroyBinTree(&((*PtrBT)->Right));
		free(*PtrBT);
        *PtrBT=NULL;
	}
}/* Num:2 */

void CreateBinTree(BinTree *PtrBT)
{
	char value;
	scanf("%c",&value);
	if(value=='^') 
	{
		*PtrBT=NULL;	/*建空二叉树*/
	}
	else
	{
		*PtrBT=(BinTree)malloc(sizeof(TreeNode));
		(*PtrBT)->Data=value;
        CreateBinTree(&((*PtrBT)->Left));
        CreateBinTree(&((*PtrBT)->Right));
    }
}/* Num:3 */

void ClearBinTree(BinTree *PtrBT)
{
	if(*PtrBT)
	{
		(*PtrBT)->Data='^';
		ClearBinTree(&((*PtrBT)->Left));
		ClearBinTree(&((*PtrBT)->Right));
	}
}/* Num:4 */

int IsEmptyBinTree(BinTree BT)
{
	return(BT->Data=='^');
}/* Num:5 */

int BinTreeDepth(BinTree BT)
{
	int hl, hr;
	if(!BT) return 0;	/*空二叉树深度为0*/
	else
	{
		hl=BinTreeDepth(BT->Left);	/*计算左子树深度*/
		hr=BinTreeDepth(BT->Right);	/*计算右子树深度*/
		return (hl>hr?(hl+1):(hr+1));
	}
}/* Num:6 */

BinTree Root(void)
{
	return root[Cur_Num];
}/* Num:7 */

char Value(BinTree *PtrBT)
{
	if(*PtrBT) return (*PtrBT)->Data;
	else return '^';
}/* Num:8 */

BinTree Assign(BinTree *PtrBT,char value)
{
	if(*PtrBT) (*PtrBT)->Data=value;
	return *PtrBT;
}/* Num:9 */

BinTree Parent(BinTree BT,BinTree PtrBT)
{
	if(BT==PtrBT) return NULL;
	Stack S=CreateStack();
	Push(S,BT);
	
	BinTree P=NULL;
	while(!IsEmptyS(S))
	{
		P=Pop(S);
		if(P->Left==PtrBT||P->Right==PtrBT) break;
		if(P->Left) Push(S,P->Left);
		if(P->Right) Push(S,P->Right);
	}
	return P;
}/* Num:10 */

BinTree LeftChild(BinTree PtrBT)
{
	if(!PtrBT->Left) return PtrBT;
	else return PtrBT->Left;
}/* Num:11 */

BinTree RightChild(BinTree PtrBT)
{
	if(!PtrBT->Right) return PtrBT;
	return PtrBT->Right;
}/* Num:12 */

BinTree LeftSibling(BinTree BT,BinTree PtrBT)
{
	BinTree P=Parent(BT,PtrBT);
	if(!P||P->Left==PtrBT) return PtrBT;
	else return P->Left;
}/* Num:13 */

BinTree RightSibling(BinTree BT,BinTree PtrBT)
{
	BinTree P=Parent(BT,PtrBT);
	if(!P||P->Right==PtrBT) return PtrBT;
	else return P->Right;
}/* Num:14 */

void InsertChild(BinTree *PtrBT,char LR, int Num)
{
    BinTree BT;
    if(LR=='L')
    {
        BT=(*PtrBT)->Left;
        (*PtrBT)->Left=root[Num];
        root[Num]->Right=BT;    
    }
    if(LR=='R')
    {
        BT=(*PtrBT)->Right;
        (*PtrBT)->Right=root[Num];
        root[Num]->Right=BT;
    }
}/* Num:15 */

void DeleteChild(BinTree *PtrBT,char LR)
{
	if(LR=='L') DestroyBinTree(&((*PtrBT)->Left));
	if(LR=='R') DestroyBinTree(&((*PtrBT)->Right));
}/* Num:16 */

void PreOrderTraverse(BinTree BT)
{
	if(BT)
	{
		printf("%c",BT->Data);
		PreOrderTraverse(BT->Left);
		PreOrderTraverse(BT->Right);
	}
}/* Num:17 */

void InOrderTraverse(BinTree BT)
{
	Stack S= CreateStack(); /*创建并初始化堆栈S*/
	while(BT||!IsEmptyS(S))
	{
		while(BT)/*一直向左并将沿途结点压入堆栈*/
		{
			Push(S,BT);
			BT=BT->Left;
		}
		if(!IsEmptyS(S))
		{
			BT=Pop(S);/*结点弹出堆栈*/
			printf("%c",BT->Data);/*(访问)打印结点*/
			BT=BT->Right;/*转向右子树*/
		}
	}
}/* Num:18 */

void PostOrderTraverse(BinTree BT)
{
	if(BT)
	{
		PostOrderTraverse(BT->Left);
		PostOrderTraverse(BT->Right);
		printf("%c",BT->Data);
	}
}/* Num:19 */

void LevelOrderTraverse(BinTree BT)
{
	Queue Q;
    BinTree T;
	if(!BT) return;/*若是空树直接返回*/
	Q=CreateQueue();/*创建并初始化队列Q*/
	AddQ(Q,BT);
	while(!IsEmptyQ(Q))
	{
		T=DeleteQ(Q);
		printf("%c",T->Data);/*访问取出队列的结点*/
		if(T->Left) AddQ(Q,T->Left);
		if(T->Right) AddQ(Q,T->Right);
	}
}/* Num:20 */

_Bool SetBTNum(void)
{
	int in_Num;
	scanf("%d",&in_Num);
	if(in_Num>=0&&in_Num<NR)
	{
		Cur_Num=in_Num;
		return TRUE;
	}
	else return FALSE;
}/* Num:29 */

void CreateHTree(HTree *PtrBT)
{
	char value;
	scanf("%c",&value);
	if(value=='^') 
	{
		*PtrBT=NULL;	/*建空二叉树*/
	}
	else
	{
		*PtrBT=(HTree)malloc(sizeof(HTreeNode));
		(*PtrBT)->Data=value;
        (*PtrBT)->Parent=Parent(root[Cur_Num],*PtrBT);
        CreateHTree(&((*PtrBT)->Left));
        CreateHTree(&((*PtrBT)->Right));
    }
}/* Num:31 */

void IndexTable(HTree BT,IndexLink *PtrHC)
{
    IndexLink head=(IndexLink)malloc(sizeof(IndexNode));
    head->Next=NULL;
    IndexLink L=head;
    int length;
    int i;
    char temp;
	Stack S= CreateStack(); /*创建并初始化堆栈S*/
	while(BT||!IsEmptyS(S))
	{
		while(BT)/*一直向左并将沿途结点压入堆栈*/
		{
			Push(S,BT);
			BT=BT->Left;
		}
		if(!IsEmptyS(S))
		{
			BT=Pop(S);/*结点弹出堆栈*/
			if(BT->Left==NULL&&BT->Right==NULL)
            {
                HTree TEMP=BT;
                L->Next=(IndexLink)malloc(sizeof(IndexNode));
                L=L->Next;
                L->Data=BT->Data;
                memset(L->Code,'\0',MAXSIZE);
                for(length=0;BT!=root[Cur_Num];)
                {
                    HTree Pre=BT;
                    BT=BT->Parent;
                    if(BT->Left==Pre) L->Code[length++]='0';
                    else L->Code[length++]='1';
                }
                for(i=0;i<strlen(L->Code)/2;i++)
                {
                    temp=L->Code[i];
                    L->Code[i]=L->Code[strlen(L->Code)-i-1];
                    L->Code[strlen(L->Code)-i-1]=temp;
                }
                BT=TEMP;
            }
			BT=BT->Right;/*转向右子树*/
        }
    }
    L=NULL;
    *PtrHC=head;
}

void HTreeCode(char * str,char * code,IndexLink HC)
{
    IndexLink L;
    int ptr_str=0;
    int ptr_code=0;
    while(*(str+ptr_str)!='\0')
    {
        L=HC->Next;
        while(L->Data!=*(str+ptr_str)&&L!=NULL)
        {
            L=L->Next;
        }
        if(!L) return;
        /*find*/
        strcpy(code+ptr_code,L->Code);
        ptr_code+=strlen(L->Code);
        ptr_str++;
    }
}/* Num:32 */

void HTreeDecode(char * str,char * code,IndexLink HC)
{
    IndexLink L;
    int match;
    int ptr_str=0;
    int ptr_code=0;
    int offset;
    while(*(code+ptr_code)!='\0')
    {
        match=0;
        L=HC->Next;
        while(L&&!match)
        {
            for(offset=0;offset<strlen(L->Code);offset++)
            {
                if(*(code+ptr_code+offset)==*(L->Code+offset)) match=1;
                else 
                {
                    match=0;
                    break;
                }
            }
            if(!match) L=L->Next;
        }
        if(!L) return;
        /*find*/
        *(str+ptr_str)=L->Data;
        ptr_code+=strlen(L->Code);
        ptr_str++;
    }
}/* Num:33 */

_Bool StringCheck(char *str,IndexLink HC)
{
    char ENCODE[4*STRLEN];
    char DECODE[STRLEN];
    memset(ENCODE,'\0',4*STRLEN);
    memset(DECODE,'\0',STRLEN);
    HTreeCode(str,ENCODE,HC);   /* str=>ENCODE */
    HTreeDecode(DECODE,ENCODE,HC);  /*ENCODE=>DECODE*/
    return (strcmp(str,DECODE)==0);
}/* Num:34 */

_Bool CodeCheck(char *code,IndexLink HC)
{
    char DECODE[STRLEN];
    char ENCODE[4*STRLEN];
    memset(DECODE,'\0',STRLEN);
    memset(ENCODE,'\0',4*STRLEN);
    HTreeDecode(DECODE,code,HC);    /*code=>DECODE*/
    HTreeCode(DECODE,ENCODE,HC);    /*DECODE=>ENCODE*/
    return (strcmp(code,ENCODE)==0);
}/* Num:35*/

int main(void)
{  
    int i;
    int op=1;
    int Num;
    Cur_Num=1;  /*Default*/
    int status;
    char value;
    char LR;
    BinTree Cur_BT=NULL;
    BinTree Pre_BT=NULL;
    BinTree PRESERVED_BT[NR];
    IndexLink HC=NULL;
    IndexLink L=NULL;
    char IN_str[STRLEN];
    char OUT_code[4*STRLEN];
    char IN_code[4*STRLEN];
    char OUT_str[STRLEN];
    char *find;
    for(i=0;i<NR;i++)
    {
        PRESERVED_BT[i]=NULL;
    }
   	
    while (op) 
    {
	    system("clear");	
        printf("\n\n");
		printf("      Menu for Binary Tree On Doubly Linked List \n");
		printf("------------------------------------------------------\n");
		printf("      1. InitBinTree            2. DestroyBinTree\n");   
		printf("      3. CreateBinTree          4. ClearBinTree\n");
		printf("      5. IsEmptyBinTree         6. BinTreeDepth\n");
		printf("      7. Root                   8. Value\n");
		printf("      9. Assign                10. Parent\n");
		printf("     11. LeftChild             12. RightChild\n");  
		printf("     13. LeftSibling           14. RightSibling\n");
		printf("     15. InsertChild           16. DeleteChild\n");          
        printf("     17. PreOrderTraverse      18. InOrderTraverse\n");
        printf("     19. PostOrderTraverse     20. LevelOrderTraverse\n"); 
		printf("     29. SetBTNum              31. CreateHTree\n");
        printf("     32. HTreeCode             33. HTreeDecode\n");
        printf("     34. StringCheck           35. CodeCheck\n");
        printf("------------------------------------------------------\n");
		printf("       当前操作的树序号：%d   请选择你的操作[0~35]:\n",Cur_Num);
		scanf("%d",&op);
        getchar();
		switch(op) 
        {
		case 1:
			status=InitBinTree(&root[Cur_Num]);
            Cur_BT=root[Cur_Num];
            if(status==TRUE) printf("二叉树初始化成功\n");
            else printf("二叉树初始化失败\n");
			getchar();
			break;
		case 2:
			DestroyBinTree(&root[Cur_Num]);
            if(!root[Cur_Num]) printf("二叉树销毁成功\n");
            else printf("二叉树销毁失败\n");
			getchar();
			break;
		case 3:
            CreateBinTree(&root[Cur_Num]);
            Cur_BT=root[Cur_Num];
            if(Cur_BT) printf("二叉树创建成功\n");
            else printf("二叉树创建失败\n");
            getchar();
			getchar();
			break;
		case 4:
			ClearBinTree(&root[Cur_Num]);
            if(root[Cur_Num]->Data=='^') printf("二叉树清空成功\n");
            else printf("二叉树清空失败\n");
            Cur_BT=NULL;
			getchar();
			break;
		case 5:
            if(!root[Cur_Num]) printf("二叉树未创建\n");
            else if(IsEmptyBinTree(root[Cur_Num])) printf("空二叉树\n");
            else printf("二叉树非空\n");
			getchar();
			break;
		case 6:
			printf("二叉树的深度是%d\n",BinTreeDepth(root[Cur_Num]));
			getchar();
			break;
		case 7:
			Cur_BT=Root();
            printf("%c\n",Value(&Cur_BT));
			getchar();
			break;
		case 8:
			value=Value(&Cur_BT);
            printf("%c\n",value);
			getchar();
			break;
		case 9:
            scanf("%c",&value);
            getchar();
			Cur_BT=Assign(&Cur_BT,value);
            if(Cur_BT&&Cur_BT->Data==value) printf("赋值成功\n");
            else printf("赋值失败\n");
			getchar();
			break;
		case 10:
		    Cur_BT=Parent(root[Cur_Num],Cur_BT);
            printf("%c\n",Value(&Cur_BT));
			getchar();
			break;
		case 11:
            Pre_BT=Cur_BT;
			Cur_BT=LeftChild(Cur_BT);
            if(Pre_BT!=Cur_BT) printf("%c\n",Value(&Cur_BT));
            else printf("^\n");
            Pre_BT=NULL;
		    getchar();
			break;
		case 12:
            Pre_BT=Cur_BT;
			Cur_BT=RightChild(Cur_BT);
            if(Pre_BT!=Cur_BT) printf("%c\n",Value(&Cur_BT));
            else printf("^\n");
            Pre_BT=NULL;
			getchar();
			break;
		case 13:
            Pre_BT=Cur_BT;
			Cur_BT=LeftSibling(root[Cur_Num],Cur_BT);
            if(Pre_BT!=Cur_BT) printf("%c\n",Value(&Cur_BT));
            else printf("^\n");
            Pre_BT=NULL;
			getchar();
			break;
		case 14:
            Pre_BT=Cur_BT;
			Cur_BT=RightSibling(root[Cur_Num],Cur_BT);
            if(Pre_BT!=Cur_BT) printf("%c\n",Value(&Cur_BT));
            else printf("^\n");
            getchar();
			break;
		case 15:
            printf("请输入左(L)/右(R)以及二叉树序号\n");
			scanf("%c %d",&LR,&Num);
            getchar();
            InsertChild(&Cur_BT,LR,Num);
            if(root[0]) 
            {
                DestroyBinTree(&root[0]);
            }
            getchar();
			break;
		case 16:
			printf("请输入左(L)/右(R)\n");
            scanf("%c",&LR);
            getchar();
            DeleteChild(&Cur_BT,LR);
            getchar();
			break;
		case 17:
			PreOrderTraverse(root[Cur_Num]);
			getchar();
			break;
		case 18:
			InOrderTraverse(root[Cur_Num]);
			getchar();
			break;
        case 19:
            PostOrderTraverse(root[Cur_Num]);
            getchar();
            break;
        case 20:
            LevelOrderTraverse(root[Cur_Num]);
            getchar();
            break;
        case 29:
            if(Cur_BT) PRESERVED_BT[Cur_Num]=Cur_BT;
            status=SetBTNum();
            if(PRESERVED_BT[Cur_Num]) Cur_BT=PRESERVED_BT[Cur_Num];
            else Cur_BT=root[Cur_Num];
            if(status==TRUE) printf("位序设置成功\n");
            else printf("位序设置失败\n");
            getchar();
            getchar();
            break;
        case 31:
            CreateHTree(&root[Cur_Num]);
            Cur_BT=root[Cur_Num];
            if(Cur_BT) 
            {
                printf("哈夫曼树创建成功\n");
                IndexTable(root[Cur_Num],&HC);
            }
            else printf("哈夫曼树创建失败\n");
            getchar();
            getchar();
            break;
        case 32:
            memset(IN_str,'\0',STRLEN);
            memset(OUT_code,'\0',4*STRLEN);
            for(L=HC->Next;L;L=L->Next)
            {
                printf("[%c] %s\n",L->Data,L->Code);
            }
            fgets(IN_str,STRLEN,stdin);
            find=strchr(IN_str,'\n');
            if(find)
            {
                *find='\0';
            }
            HTreeCode(IN_str,OUT_code,HC);
            printf("%s\n",OUT_code);
            getchar();
            break;
        case 33:
            memset(IN_code,'\0',4*STRLEN);
            memset(OUT_str,'\0',STRLEN);
            for(L=HC->Next;L;L=L->Next)
            {
                printf("[%c] %s\n",L->Data,L->Code);
            }
            printf("\n");
            fgets(IN_code,4*STRLEN,stdin);
            find=strchr(IN_code,'\n');
            if(find)
            {
                *find='\0';
            }
            HTreeDecode(OUT_str,IN_code,HC);
            printf("%s\n",OUT_str);
            getchar();
            break;
        case 34:
            memset(IN_str,'\0',STRLEN);
            memset(OUT_code,'\0',4*STRLEN);
            fgets(IN_str,STRLEN,stdin);
            find=strchr(IN_str,'\n');
            if(find)
            {
                *find='\0';
            }
            printf("%d\n",StringCheck(IN_str,HC));
            getchar();
            break;
        case 35:
            memset(IN_code,'\0',4*STRLEN);
            memset(OUT_str,'\0',STRLEN);
            fgets(IN_code,4*STRLEN,stdin);
            find=strchr(IN_code,'\n');
            if(find)
            {
                *find='\0';
            }
            printf("%d\n",CodeCheck(IN_code,HC));
            getchar();
            break;
		case 0:
			break;
		}
	}
	printf("欢迎下次再使用本系统！\n");
	return 0;
}





	

