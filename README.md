# M1_project_Tree Data Structure


Introduction-
                    
                    
                    A tree data structure can be defined recursively as a collection of nodes, where each node is a data structure consisting of a value and a list of references to nodes. The start of the tree is the "root node" and the reference nodes are the "children". No reference is duplicated and none points to the root.


Feautures and Benefits-
                      
                      
                      1.Insert
                      2.Delete
                      3.Inorder Traversal
                      4.Preorder Traversal
                      5.Postorder Traversal
                      


Explanation-
                     
                     
                     A tree data structure is a non-linear data structure because it does not store in a sequential manner. It is a hierarchical structure as elements in a Tree are arranged in multiple levels. In the Tree data structure, the topmost node is known as a root node. Each node contains some data, and data can be of any type.
                     
                     
Code-

     #include<stdio.h>
#include<stdlib.h>
struct node
{
	int data;
	struct node *left;
	struct node*right;
};
struct node *insert(struct node *,int);
struct node *deletenode(struct node *, int);
void inorder(struct node*);
void preorder(struct node*);
void postorder(struct node*);
int main()
{
 int data,choice,wish;
 struct node *root=NULL;
 do
 {
    	printf("\n\n");
        printf("\t-----------------TREE DATA STRUCTURE OPERATIONS----------------\n");
        printf("\t============================================================\n");
        printf("\t 1.Insert\n");
        printf("\t 2.Deletion\n");
        printf("\t 3.Inorder Traversal\n");
        printf("\t 4.Preorder Traversal\n");
        printf("\t 5.Postorder Traversal\n");
        printf("\t============================================================\n");
        printf("\t  Enter Your Option :");
        scanf("%d",&choice);
        switch(choice)
    {
     case 1:
                 printf("Enter the element to insert : ");
                 scanf("%d",&data);
                 root = insert(root,data);
                 printf("%d ",data);
                 break;
    case 2:
                 printf("Enter the element to delete : ");
                 scanf("%d",&data);
                 root = deletenode(root,data);
                 break;
     case 3:
                 inorder(root);
                 break;
     case 4:
                 preorder(root);
                 break;
     case 5:
     postorder(root);
                 break;
     default:
                 printf("WRONG CHOICE");
  }
  printf("\nDo you want to continue(0/1): ");
  scanf("%d",&wish);
 }while(wish);
 return 0;
}
struct node *createnode(value)
{
	struct node *newnode=malloc(sizeof(struct node));
	newnode->data=value;
	newnode->left=NULL;													
	newnode->right=NULL;
	return newnode;
}
struct node* insert(struct node* root,int data)
{
	if(root==NULL){
	
	return createnode(data);
	}
	if(data < root->data){
	
	root->left=insert(root->left,data);}
	else if(data > root->data){

	
	root->right=insert(root->right,data);}
	return root;
}
void inorder(struct node* root)
{
	if(root==NULL)
	return;
	 inorder(root->left);
	 printf("%d-> ",root->data);
	 inorder(root->right);
}
void postorder(struct node* root)
{
	if(root==NULL)
	return;
	
	 postorder(root->left);
	
	 postorder(root->right);
	   printf("%d-> ",root->data);
}
void preorder(struct node* root)
{
	if(root==NULL)
	return;
	 printf("%d-> ",root->data);
	 preorder(root->left);
	 preorder(root->right);

}
struct node* FindMin(struct node* node)
{ 
	struct node* current = node; 

	
	while (current && current->left != NULL) 
		current = current->left; 

	return current; 
} 
struct node* deletenode(struct node *root,int data)
{
	if(root==NULL){
	
	return root;
	}
	else if(data < root->data){
	
	root->left=deletenode(root->left,data);}
	else if(data > root->data){

	
	root->right=deletenode(root->right,data);}
	else
	{
		if(root->left==NULL&&root->right==NULL)
		{
			free(root);
			root=NULL;
			return root;
		}
		else if(root->left==NULL)
		{
			struct node *temp=root;
			root=root->right;
			free(temp);
		}
		else if(root->right==NULL)
		{
			struct node *temp=root;
			root=root->left;
			free(temp);
		}
		else
		{
			struct node *temp= FindMin(root->right);
			root->data=temp->data;
			root->right=deletenode(root->right,temp->data);
		}
	}
	return root;
}
            
